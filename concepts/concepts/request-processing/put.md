# PUT Requests

Typically, an endpoint for PUT requests is build up like this:

```
/<application>/<applicationVersion>/<entityName Plural>/<entity id>/
```

For example

```
/mynotesApp/v1/notes/17/
```

The actual class dealing with the request is derived from PutEntityServerResource and could look something like this:

```java
public class PutNoteResource extends PutEntityServerResource<Note> {

    protected String id;
    protected NotesApplication app;

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



