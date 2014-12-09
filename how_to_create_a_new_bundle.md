# How to... create a new bundle project

### Assumptions

This How-to assumes that you have set up eclipse with bndtools and checkout the set of skysail projects.

### Example

For this example, let's assume we want to create a new skysail application which is able to parse a directory structure for mp3 files, list them and let's the user play them.

### Creating the project

In eclipse, in the package explorer, right-click and choose *New* > *Bndtools OSGi Project*. Leave the defaults, name it *skysail.server.app.music*. On the next page, select *Empty Project* as Project Template. Click finish.

Open the bnd.bnd file and edit it so that it looks like this:

```
Bundle-Name: SKYSAIL :: server :: app :: wiki
Bundle-Version: 0.0.1.${tstamp}
Service-Component: *
Include-Resource: resources, templates=src;recursive:=true;filter:=*.st|*.stg
-buildpath: biz.aQute.bnd.annotation,\
	skysail.api;version=${skysail.api.version},\
	skysail.server;version=${skysail.server.version},\
	slf4j.api;version=1.7.7,\
	org.restlet;version=${restlet.version},\
	skysail.server.app.i18n;version=latest,\
	javax.validation.api;version=1.1,\
	javax.persistence;version=2.1
Import-Package: org.osgi.framework,\
	javassist.util.proxy,\
	*
```


