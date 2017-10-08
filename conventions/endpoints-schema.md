### Endpoints' schema

There's a certain semantic in the way skysail defines endpoints for request processing, let's explain this with a little example of a note handling application with an entity "Note".

The dots in the endpoint definition stand for "/&lt;application name&gt;/&lt;application version&gt;", so that the actual endpoint for the PutEntityServerResource would look like "[https://&lt;server&gt;:&lt;port&gt;/notesapp/v1/notes/27/](https://<server>:<port>/notesapp/v1/notes/27/)".

| Endpoint | Resource Type | Verbs | Description |
| :--- | :--- | :--- | :--- |
| **.../notes** | [AsyncListResource](https://github.com/evandor/skysail-core/blob/master/skysail.core/src/io/skysail/core/resources/AsyncListResource.scala) | GET | This endpoint provides a list view of all notes \(optionally using filtering and pagination |
|  |  | DELETE | A delete request for all \(optionally filtered\) notes |
| ...**/notes/** | AsyncPostResource | POST | Creates a new Note |
|  |  | GET | Returns a representation of a Note which can be used as template for posting. |
| ...**/notes/{id}** |  | GET | Returns a representation of the entity \(here: note\) for the given id. |
|  |  | DELETE | Deletes the entity with the provided id. |
| ...**/notes/{id}/** | AsyncPutResource | PUT | Updates the entity with the given id. |
|  |  | GET | Returns a representation of the entity which can be used for a PUT request. |



