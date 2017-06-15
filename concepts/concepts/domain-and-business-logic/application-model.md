# Application Model

**This is the core domain of skysail: **

A model describing an _application_, consisting of _resources_, associated _entities_ \(with _fields_\) and _links_ between resources.

You do not need to know a lot about these models if you just want to use or write SkysailApplications, but a general understanding is helpful to understand the features \(and also limitations\) of skysail applications.

## Overview

_skysail_ is something like a runtime environment for [_SkysailApplications_](/concepts/concepts/applications.md). Whenever such an Application is started, a model describing that application will be created, and this model will be used to determine which resources are available under which path, what kind of entities can be created, updated and deleted and so on.

![](/assets/solutionDomain.png)

The most recent code documentation for the Application Model can be found [here](http://jenkins.twentyeleven.de/view/pipelines/job/skysail-core.pipeline/Scaladoc/index.html#io.skysail.core.model.package).

### Application Models

An ApplicationModel is created like this:

```
val appModel = ApplicationModel("appName", ApiVersion(1), associatedResourceClassesList)
```

This is done in the constructor of a _SkysailApplication, _and it associates this application with its model. 

Now, suppose you attach a new resource to the application as usual in the attach-Method of _SkysailApplication:_

```java
 override def attach() = {
   router.attach(new RouteBuilder("/bookmarks", classOf[BookmarksResource]))
   ...
 }
```

This results is a call in _SkysailRouter\#addResourceModel_ updating the application model:

```
 appModel.addResourceModel("/bookmarks", classOf[BookmarksResource])

```

Now, _BookmarksResource_ is analyzed and found to be parameterized with the entity _Bookmark _or, more precise: _List\[Bookmark\]_:

```
class BookmarksResource extends ListServerResource[List[Bookmark]] ... { ... }
```

In effect, the _BookmarksResource_ is added to the _resourceModels_ list of the applicationModel, and a new Entity - if it did not exist yet - is added to the _entityModelsMap_. This map associates the entity class name and its _EntityModel_.

### EntityModels

An entityModel can be created from any class, but typically these will be instances of _SkysailEntity_. The classes fields will be analyzed, and for the ones being annotated with "_io.skysail.core.html.Field_", FieldModels will be created and added to the _EntityModel's_ fields memeber.

### FieldModels

### ResourceModels

### LinkModels



