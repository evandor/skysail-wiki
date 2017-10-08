# Request Handling

## RoutesCreator \(Actor\):

Matches the request to a Handler via the requests URI, applying a series of common Directives \(to deal with authentication, content negotiation etc\). 

If a match is found, a new _ProcessComand_ message is sent to the associated application actor: 

```scala
val applicationActor: ApplictionActor = ...
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

```
case cmd: ProcessCommand => {
  val sendBackTo = sender()
  val theClass = cmd.cls.newInstance()
  val controllerActor = ... // create new ControllerActor as Child
  val r = (controllerActor ? SkysailContext(cmd, appModel, theClass, bundleContext)).mapTo[ListResponseEvent[_]]
  r onComplete {
    case Success(value) => sendBackTo ! value
    case Failure(failure) => ...
  }
}

```



## ControllerActor

```
cmd.ctx.request.method match {
  case HttpMethods.GET =>
  case HttpMethods.PUT =>
  case HttpMethods.DELETE => 
  case HttpMethods.POST => resource.asInstanceOf[PostSupport].post(RequestEvent(cmd, self))
  case e: Any => resource.get(RequestEvent(cmd, self))
}
```

## Resource

```
def get(requestEvent: RequestEvent): Unit = {
    val applicationActor = SkysailApplication.getApplicationActorSelection(actorContext.system, classOf[BookmarksApplication].getName)
    val r = (applicationActor ? ApplicationActor.GetApplication()).mapTo[BookmarksApplication]
    //reply(requestEvent, app.repo.find())
    r onComplete {
      case Success(app) => requestEvent.controllerActor ! ListResponseEvent(requestEvent, app.repo.find())
      case Failure(failure) => println(failure)
    }
  }
}
```

## ControllerActor

    case response: ListResponseEvent[T] =>
      val negotiator = new MediaTypeNegotiator(response.req.cmd.ctx.request.headers)
      val acceptedMediaRanges = negotiator.acceptedMediaRanges

      implicit val formats = DefaultFormats
      implicit val serialization = jackson.Serialization

      val m = Marshal(response.resource.asInstanceOf[List[_]]).to[RequestEntity]

      if (negotiator.isAccepted(MediaTypes.`text/html`)) {
        handleHtmlWithFallback(response, m)
      } else if (negotiator.isAccepted(MediaTypes.`application/json`)) {
        handleJson(m, response)
      }
    case response: ResponseEvent[T] =>
      val negotiator = new MediaTypeNegotiator(response.req.cmd.ctx.request.headers)
      val acceptedMediaRanges = negotiator.acceptedMediaRanges

      implicit val formats = DefaultFormats
      implicit val serialization = jackson.Serialization

      //val m = Marshal(response.resource).to[RequestEntity]

      val e = Extraction.decompose(response.resource).asInstanceOf[JObject]
      val written = write(e)

      if (negotiator.isAccepted(MediaTypes.`text/html`)) {
        handleHtmlWithFallback(response, e)
      } else if (negotiator.isAccepted(MediaTypes.`application/json`)) {
        //handleJson(m,response)
      }



