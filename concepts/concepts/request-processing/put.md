# PUT Requests

Typically, an endpoint for PUT requests is build up like this:

```
/<application>/<applicationVersion>/<entityName Plural>/<entity id>/
```

For example

```
/mynotesApp/v1/notes/17/
```

The actual class dealing with the request is derived from _PutEntityServerResource_ and could look something like this:

```java
public class PutNoteResource extends PutEntityServerResource<Note> {

    private String id;
    private NotesApplication app;

    @Override
    protected void doInit() throws ResourceException {
        app = (NotesApplication)getApplication();
    }

    @Override
    public void updateEntity(Note  entity) {
        Note original = getEntity();
        copyProperties(original,entity);
        app.getRepository().update(original,null);
    }

    @Override
    public Note getEntity() {
        return app.getRepository().findOne(getAttribute("id"));
    }

    @Override
    public String redirectTo() {
        return super.redirectTo(NotesResource.class);
    }
}
```

The _PutNoteResource_ classes purpose is to

* provide the concrete entity for the id taken from the url \(GET request\)
* update the entity defined by the id in the URL \(PUT request\)

* define the redirect url \(where you will be redirected after a successful PUT request\)

All other logic is defined in the parent class, _PutEntityServerResource_.

### Request Handling

##### @Put \(www-form-urlencoded\)

The signature of the method handling the request looks like this:

```
@org.restlet.resource.Put("x-www-form-urlencoded")
public SkysailResponse<T> put(Form form, Variant variant) {...}
```

The logic:

1. Wrap the request in a timer [metric](/metrics.md).
2. Deserialise the provided \(Restlet\) Form
3. Follow the @Put\(JSON\) logic

##### @Put \(JSON\)

The signature of the method handling the request looks like this:

```
@Put("json")
public SkysailResponse<T> putEntity(T entity, Variant variant) {...}
```

The logic:

1. Wrap the request in a timer metric.
2. Add entity and variant to the request attributes for further consumption
3. Get the request handler for PUT requests and apply the following filters:
   [ExceptionCatchingFilter](/concepts/concepts/request-processing/filtering/exceptioncatchingfilter.md) - handle exceptions during request processing  
   ExtractStandardQueryParametersResourceFilter - check and update common query parameters  
   CheckInvalidInputFilter - security check for invalid input   
   FormDataExtractingFilter - extract the entity  
   CheckBusinessViolationsFilter - validate the entity according to business rules  
   UpdateEntityFilter - trigger persistence logic to update the entity in the repository  
   EntityWasAddedFilter - handle update events  
   AddLinkheadersFilter - add link information to response headers  
   PutRedirectGetFilter - make sure request cannot be resubmitted accidentally  



