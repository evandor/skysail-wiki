# Conventions

skysail consists of a number of bundles and depends on various others. In order to make things clearer and more consistent, there are a couple of conventions skysail code sticks to \(with little exceptions\):

### skysail Bundles

A skysail **bundle's symbolic name** starts with "_skysail._", followed by

* "api"
* "domain"
* "core"
* "app"
* to be done

The **bundle's name** has the naming convention "SKYSAIL :: &lt;type&gt; :: &lt;futher parts&gt;"

### bundle versions

skysail uses a semantic versioning scheme.

### skysail packages

skysail packages always start with "io.skysail.&lt;type&gt;.&lt;futher parts&gt;".

### endpoints

There's a certain semantic in the way skysail defines endpoints for request processing, let's explain this with a little example of a note handling application with an entity "Note":

| Endpoint | Resource Type  | Verbs | Description |
| :--- | :--- | :--- | :--- |
| **/notes** | ListServerResource | GET | This endpoint provides a list view of all notes \(optionally using filtering and pagination |
|  |  | DELETE | A delete request for all \(optionally filtered\) notes |
| **/notes/** | PostEntityServerResource | POST | Creates a new Note |
|  |  | GET | Returns a representation of a Note which can be used as template for posting. |
| **/notes/{id}** | EntityServerResource | GET | Returns a representation of the entity \(here: note\) for the given id. |
|  |  | DELETE | Deletes the entity with the provided id. |
| **/notes/{id}/** | PutEntityServerResource | PUT | Updates the entity with the given id. |
|  |  | GET | Returns a representation of the entity which can be used for a PUT request. |





