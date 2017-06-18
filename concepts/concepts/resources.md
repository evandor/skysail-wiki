# Resources

Resources play a crucial role in REST. Restlet, being the framework skysail builds upon, defines a class "_org.restlet.resource.ServerResource_" which should be extended to implement server-side resources. skysail extends this class with "_SkysailServerResource_" and resources in skysail typically extend the latter class.

Restlet does not tell you how exactly your resources should look like, you have all the freedom, but you have to make up your mind yourself. skysails "SkysailServerResource" class is abstract and provides some default implementations:

![](/assets/skysailServerResources.png)

The idea is to provide you with a set of [conventions](/conventions.md) and associated resources to handle the typical tasks of creating, altering, listing and deleting resources, no need to reinvent the wheel all the time.

**Let's just do a simple example: **

Let's say you want to create a Checklist Application. The domain of this application will need a Checklist Entity, something which will look like

```
class Checklist {
  val title: String,
  val elements: List[String]  
}
```

Now, you want to create a new Checklist. You'd provide a class extending _PostEntityServerResource\[Checklist\]_:

```
class PostChecklistResource extends PostEntityServerResource[Checklist] {
  def createEntityTemplate() = Checklist("mylist", List())
  def addEntity(entity: Checklist): Checklist = Services.service.create(entity).get
}
```

This class - provided the service which will actually create the entity - is sufficient to handle requests to create a Checklist.

The Checklist has been created - but now you want to **list** all Checklists available: Implement a _ListServerResource_:

```java
class ChecklistsResource extends ListServerResource[List[Checklist]] {
  override def getEntity() = Services.service.find(new Filter(getRequest()), new Pagination(getRequest(), getResponse()))
}
```

Again, that's it. This class will list all available Checklists. Change a checklist? Here we go:

```java
class PutChecklistResource extends PutEntityServerResource[Checklist] {
  addToContext(ResourceContextId.LINK_TITLE, "update Checklist")
  override def getEntity(): Checklist = Services.service.getById(getAttribute("id")).get
  def updateEntity(entity: Checklist): Checklist = {
    val original = getEntity()
    copyProperties(original, entity)
    entity.id = original.id
    Services.service.update(entity).get
  }
}
```

Let's show the service implementation as well:

```java
object Services {
  def service = org.restlet.Application.getCurrent().asInstanceOf[ChecklistsApplication].service
}

class ChecklistsService(dbService: ScalaDbService, appModel: ApplicationModel) {

  private var repo = new ChecklistsRepository(dbService)
  private implicit val formats = DefaultFormats

  private var i = 0

  def create(car: Checklist): Try[Checklist] = repo.save(car, appModel)
  def update(car: Checklist): Try[Checklist] = repo.update(car, appModel)

  def getById(id: String): Option[Checklist] = {
    val entry = repo.findOne(id)
    if (entry.isDefined) Some(entry.get.extract[Checklist]) else None
  }

  def find(f: Filter, p: Pagination) = repo.find(f, p).map { row => row.extract[Checklist] }.toList

}
```

Finally, to make this actually run, we need an [Application:](/concepts/concepts/applications.md)

```java
@Component(
  immediate = true,
  configurationPolicy = ConfigurationPolicy.OPTIONAL,
  service = Array(classOf[ApplicationProvider]))
class ChecklistsApplication extends SkysailApplication("checklists",new ApiVersion(int2Integer(1))) {

  var service: ChecklistsService = null

  @Reference(cardinality = ReferenceCardinality.MANDATORY)
  var dbService: ScalaDbService = null

  @Reference(policy = ReferencePolicy.DYNAMIC, cardinality = ReferenceCardinality.OPTIONAL)
  def setApplicationListProvider(service: ScalaServiceListProvider) {
    SkysailApplication.serviceListProvider = service;
  }

  def unsetApplicationListProvider(service: ScalaServiceListProvider) {
    SkysailApplication.serviceListProvider = null;
  }

  @Activate
  override def activate(appConfig: ApplicationConfiguration, componentContext: ComponentContext) = {
    super.activate(appConfig, componentContext);
    service = new ChecklistsService(dbService, getApplicationModel2())
  }

  override def attach() = {
    router.attach(new RouteBuilder("", classOf[ChecklistsResource]))
    router.attach(new RouteBuilder("/Checklists", classOf[ChecklistsResource]))
    router.attach(new RouteBuilder("/Checklists/", classOf[PostChecklistResource]))
    router.attach(new RouteBuilder("/Checklists/{id}", classOf[ChecklistResource]))
    router.attach(new RouteBuilder("/Checklists/{id}/", classOf[PutChecklistResource]))

    createStaticDirectory();
  }

  override def defineSecurityConfig(securityConfigBuilder: SecurityConfigBuilder) = {
    securityConfigBuilder.authorizeRequests().startsWithMatcher("").permitAll();
  }

}
```



