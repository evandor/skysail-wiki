# ListServerResource\[T\]

If you havn't read the intro about skysail resources, you'll find it [here](/resources.md).

### Overview

A _ListServerResource_ is a _SkysailServerResource_ parameterized with a **List** of some Type. It's purpose is to provide endpoints for listing multiple entities of the same kind: Implementing a specific ListServerResource could, for example, give you a list of notes, customers, connections, whatever.

These lists can be paginated and sorted, and they can be retrieved as html, json, xml and so on.

### Example

Let's create a list of Notes, which are defined as

```
case class Note (
    var id: Option[String] = None,
    @(Field @field)(description = "The note's content") 
    @BeanProperty var content: String = ""
) extends ScalaEntity[String]  
```

The ListServerResource would look like

```
class NotesResource extends ListServerResource[List[Note]](classOf[NoteResource]) {
  setDescription("resource class responsible of handling requests to get the list of all notes")
  addToContext(ResourceContextId.LINK_TITLE, "list Notes");
  override def linkedResourceClasses() = List(classOf[PostNoteResource])

  @ApiSummary("returns the (potentially filtered, sorted and paginated) notes")
  @ApiDescription("some description")
  @ApiTags(Array("Note","Testing Swagger"))
  def getEntity(): List[Note] = {
    implicit val formats = DefaultFormats
    val filter = new Filter(getRequest());
    val pagination = new Pagination(getRequest(), getResponse());
    val result = NotesResource.noteRepo(getSkysailApplication()).find(filter, pagination)
    result.map { row => row.extract[Note] }.toList
  }
}
```

setDescription and the @ApiXXX Annotations are optional and being used by the swagger extension.

