# POST Requests

Typically, an endpoint for POST requests is build up like this:

```
/<application>/<applicationVersion>/<entityName Plural>/
```

For example

```
/mynotesApp/v1/notes/
```

The actual class dealing with the request is derived from _PutEntityServerResource_ and could look something like this:

```java
public class PutNoteResource extends PostEntityServerResource<Note> {

    private String id;
    private NotesApplication app;

    @Override
    protected void doInit() throws ResourceException {
        app = (NotesApplication)getApplication();
    }

    @Override
    public Note createEntityTemplate() {
        return new Note();
    }


    @Override
    public void addEntity(Note entity) {
        ...
    }

    @Override
    public String redirectTo() {
        return super.redirectTo(NotesResource.class);
    }
}
```

The _PostNoteResource_ classes purpose is to

* provide an entity template which can be used for the POST request \(GET request\)
* create a new entity \(POST request\) the id of which is defined by the backend

* define the redirect url \(where you will be redirected after a successful POST request\)

All other logic is defined in the parent class, _PostEntityServerResource_.

### Request Handling

##### @POST \(www-form-urlencoded\)

The signature of the method handling the request looks like this:

```
@org.restlet.resource.Post("x-www-form-urlencoded")
public SkysailResponse<T> post(Form form, Variant variant) {...}
```

The logic:

1. Wrap the request in a timer [metric](/metrics.md).
2. Deserialise the provided \(Restlet\) Form
3. Follow the @Post\(JSON\) logic

##### @POST \(JSON\)

The signature of the method handling the request looks like this:

```
@Post("json")
public SkysailResponse<T> post(T entity, Variant variant) {...}
```

The logic:

1. Wrap the request in a timer metric.
2. Add entity and variant to the request attributes for further consumption
3. Get the request handler for POST requests and apply the following filters:
   [ExceptionCatchingFilter](/concepts/concepts/request-processing/filtering/exceptioncatchingfilter.md) - handle exceptions during request processing  
   ExtractStandardQueryParametersResourceFilter - check and update common query parameters  
   [CheckInvalidInputFilter](/concepts/concepts/request-processing/filtering/checkinvalidinputfilter.md) - security check for invalid input   
   FormDataExtractingFilter - extract the entity  
   [CheckBusinessViolationsFilter](/concepts/concepts/request-processing/filtering/checkbusinessviolationsfilter.md) - validate the entity according to business rules  
   PersistEntityFilter - trigger persistence logic to update the entity in the repository  
   EntityWasAddedFilter - handle update events  
   AddLinkheadersFilter - add link information to response headers  
   PostRedirectGetFilter - make sure request cannot be resubmitted accidentally  



