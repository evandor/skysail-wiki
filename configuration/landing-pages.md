# Landing Pages

### Purpose

You can define an "**entry point**" to your application, this is basically the first page a user will see. The root context for both authenticated and anonymous users can be defined.

### Config File Name

_landingpages.cfg_ \(located in one of the [configuration folders](/configuration.md)\).

### Example

```
landingPage.notAuthenticated=/pact/v1
landingPage.authenticated=/pact/v1
```

### Implementation

The landingpages configuration is evaluated in the _SkysailRootApplication_ class which is annotated like this:

```
@Component(
  property = { Array("service.pid=landingpages") },
  service = ...)
class SkysailRootApplication extends SkysailApplication(...) ... { ... }
```

Now, when the application root path is requested, this is handled by the _DefaultResource_, which is defined in the _SkysailRootApplication _class. DefaultResource overrides the redirectTo - Method 

```
override def redirectTo() = {
  getSkysailApplication().asInstanceOf[SkysailRootApplication].getRedirectTo(this);
}
```

to delegate to SkysailRootApplication.

