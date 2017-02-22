### Endpoints' schema

There's a certain semantic in the way skysail defines endpoints for request processing, let's explain this with a little example of a note handling application with an entity "Note".

The dots in the endpoint definition stand for "/&lt;note application name&gt;/&lt;application version&gt;:

| Endpoint | Resource Type | Verbs | Description |
| :--- | :--- | :--- | :--- |
| **.../notes** | ListServerResource | GET | This endpoint provides a list view of all notes \(optionally using filtering and pagination |
|  |  | DELETE | A delete request for all \(optionally filtered\) notes |
| ...**/notes/** | PostEntityServerResource | POST | Creates a new Note |
|  |  | GET | Returns a representation of a Note which can be used as template for posting. |
| ...**/notes/{id}** | EntityServerResource | GET | Returns a representation of the entity \(here: note\) for the given id. |
|  |  | DELETE | Deletes the entity with the provided id. |
| ...**/notes/{id}/** | PutEntityServerResource | PUT | Updates the entity with the given id. |
|  |  | GET | Returns a representation of the entity which can be used for a PUT request. |



