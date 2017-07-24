# Conventions

skysail consists of a number of bundles and depends on various others. In order to make things clearer and more consistent, there are a couple of conventions skysail code sticks to \(with little exceptions\):

### skysail Bundles

A skysail **bundle's symbolic name** starts with "_skysail._", followed by its "type", e.g.

* "core"
* "server"
* "app"
* "ext"
* ...

The **bundle's name** has the naming convention "SKYSAIL :: &lt;type&gt; :: &lt;futher parts&gt;".

### bundle versions

skysail uses a [semantic versioning scheme](http://bnd.bndtools.org/chapters/170-versioning.html).

### skysail packages

skysail packages always start with "io.skysail.&lt;type&gt;.&lt;futher parts&gt;".

### endpoints

There's a certain semantic in the way skysail defines endpoints for request processing, please check the next page.

