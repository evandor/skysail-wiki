# Request Handling

```
http://helenaedelson.com/?p=879
```

This

## ![](/assets/actors.png)

## 

## RoutesCreator \(Actor\):

**Matches the request to a Handler** via the requests URI, applying a series of common Directives \(to deal with authentication, content negotiation etc\). If no route is created matching a specific URI, skysail will return the usual 404 response.

Otherwise, if a match is found, **a new **_**ProcessComand**_** message is sent to the associated application actor**:

```scala
val applicationActor = ... // get the application actor for the current Application
val processCommand = ProcessCommand(requestContext, resourceClass, urlParameter, unmatchedPath)
(applicationActor ? processCommand).mapTo[ListResponseEvent[_]]
...
```

The _ProcessCommand_ is created using

* the current _akka.http.scaladsl.server.RequestContext_ 
* the resource class \(extending io.skysail.core.resources.Resource\), which defines the business logic to be executed for this request
* to be done
* the "unmatched path", which is the optional suffix of the URI which was not matched completely.

## ApplicationActor

The _ApplicationActor_ handles the ProcessCommand created by the RoutesCreator:

```scala
case cmd: ProcessCommand => {
  ...
  val theClass = cmd.resourceClass.newInstance()
  val controllerActor = ... // create new ControllerActor as Child
  (controllerActor ? SkysailContext(cmd, appModel, theClass, bundleContext)).mapTo[ListResponseEvent[_]]
  ...
}
```

It uses the resource class from the _ProcessCommand_ to create a new instance of this class \(which will be used to actually execute the business logic associated with the request\).

There is only one ApplicationActor per Application, but each request creates a new ControllerActor as a child actor to the application actor.

A new SkysailContext object is sent to the newly created ControllerActor using

* the original ProcessCommand
* the applicationModel of the current Application
* the new resource instance and
* the OSGi bundle context.

## ControllerActor

Now its the newly created ControllerActors responsibility to match the request method and call the appropriate method on the resource class:

```scala
cmd.ctx.request.method match {
  case HttpMethods.GET => resource.get(RequestEvent(cmd, self))
  case HttpMethods.PUT =>
  case HttpMethods.DELETE => 
  case HttpMethods.POST => resource.asInstanceOf[PostSupport].post(RequestEvent(cmd, self))
  case e: Any => resource.get(RequestEvent(cmd, self))
}
```

## Resource

A Resource instance is not an actor. It is called by a _ControllerActor_ to execute the business logic for this request and will send back a ResponseEvent to its original ControllerActor:

```scala
def get(requestEvent: RequestEvent): Unit = {
    val r = ... // async business logic
    r onComplete {
      case Success(success) => requestEvent.controllerActor ! ListResponseEvent(requestEvent, apply(success))
      case Failure(failure) => ...
    }
  }
}
```

Now the execution returns back in the actor chain, as the original ControllerActor is sent back a ResponseEvent or ListResponseEvent:

## ControllerActor

Depending on the request's Accept-Header, the MediaTypeNegotiator is used to determine how to actually render the retrieved Response:

```scala
case response: ListResponseEvent[T] =>
  val negotiator = new MediaTypeNegotiator(response.req.cmd.ctx.request.headers)
  val acceptedMediaRanges = negotiator.acceptedMediaRanges
  ...
  val m = Marshal(response.resource.asInstanceOf[List[_]]).to[RequestEntity]

  if (negotiator.isAccepted(MediaTypes.`text/html`)) {
    handleHtmlWithFallback(response, m)
  } else if (negotiator.isAccepted(MediaTypes.`application/json`)) {
    handleJson(m, response)
  }
case response: ResponseEvent[T] =>
  ... // similar to ListResponseEvent
```

    Somewhere in handleXXX:

    val answer = HttpEntity(ContentTypes.`text/html(UTF-8)`, <body>)
    applicationActor ! response.copy(resource = response.resource, httpResponse = response.httpResponse.copy(entity = answer))

So, the ResponseEvent is sent back up in the chain to the ApplicationActor:

# ApplicationActor

```scala
val r = ... // the async result from calling the controller actor
r onComplete {
  case Success(value) => routesCreator ! value
  case Failure(failure) => ...
}
```

Finally, the RoutesCreator gets the response:

# RoutesCreator

```
val t = ... // the async result from calling the application actor
onComplete(t) {
  case Success(result) => complete(result.httpResponse)
  case Failure(failure) => ...; complete(StatusCodes.BadRequest, failure)
}
```



