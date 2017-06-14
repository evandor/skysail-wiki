# AddLinkheadersListFilter

### Purpose

This filter - as the name implies - adds Linkheaders to the list responses. Linkheaders should be used by clients to determine which resources can be reached from the current one \([HATEOAS](https://en.wikipedia.org/wiki/HATEOAS)\).

### Implementation

The link header to be added to the response headers is determined from the \(static\) links from the application Model plus some dynamic links depending on the actual data being returned.

##### beforeHandle

```java
default
```

##### doHandle

```java
default
```

##### afterHandle

```java
  val responseHeaders = ScalaHeadersUtils.getHeaders(resource.getResponse());
  val s = resource.getClass
  val links = appModel.linksFor(s) ::: resource.runtimeLinks()
  val limitedLinks = links.map(l => l.asLinkheaderElement()).mkString(",")
  responseHeaders.add(new Header("Link", limitedLinks));
```



