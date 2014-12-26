# How to... create a new bundle project

### Assumptions

This How-to assumes that you have set up eclipse with bndtools and checked out the set of skysail projects.

### Example

For this example, let's assume we want to create a new skysail application which is able to parse a directory structure for mp3 files, list them and let's the user play them.

### Creating the project

In eclipse, in the package explorer, right-click and choose *New* > *Bndtools OSGi Project*. Leave the defaults, name it *skysail.server.app.music*. On the next page, select *Empty Project* as Project Template. Click finish.

Open the bnd.bnd file and edit it so that it looks like this:

```
Bundle-Name: SKYSAIL :: server :: app :: music
Bundle-Version: 0.0.1.${tstamp}
Service-Component: *
-buildpath: biz.aQute.bnd.annotation,\
	skysail.api;version=${skysail.api.version},\
	skysail.server;version=${skysail.server.version},\
	slf4j.api;version=1.7.7,\
	org.restlet;version=${restlet.version},\
	skysail.server.app.i18n;version=latest,\
	javax.validation.api;version=1.1,\
	javax.persistence;version=2.1,\
	com.springsource.org.junit;version=4.11,\
	de.twentyeleven.skysail.org.hamcrest.hamcrest-all-osgi;version=1.3,\
	org.mockito.mockito-all;version=1.9,\
	lombok;version=1.12,\
	etm.core;version=1.2
Import-Package: org.osgi.framework,\
	javassist.util.proxy,\
	*
```

### Creating the application

In the new project create a class called *MusicApplication* in a package of your choice, looking like this:

```
@aQute.bnd.annotation.component.Component(immediate = true)
public class MusicApplication extends SkysailApplication implements ApplicationProvider, MenuItemProvider {

	private static final String APP_NAME = "music";

	public MusicApplication() {
		super(APP_NAME);
	}

	@Override
    protected void attach() {
    }

	public List<MenuItem> getMenuEntries() {
		MenuItem appMenu = new MenuItem("Music Player", "/music");
		appMenu.setCategory(MenuItem.Category.APPLICATION_MAIN_MENU);
		return Arrays.asList(appMenu);
	}
}
```
We will fill the *attach* method later on.

For now, make sure that the new package will be added to the generated jar by opening the bnd file, switching to the *Content* tab and drag-and-dropping the source folder into
the *Private Packages* section. Save and verify that you got a 	jar file in the *generated* folder with the following contents:

to be done

#### Testing the new application

Add the new bundle to a running skysail installation (see here (tbd)); you should find a new entry in the *Applications* menu; clicking on it, though, will give you a *404 Not Found* error, as there are no routes defined yet which will deal with requests to this application. So, let's create such a route.

### A first route in our new application

Routes are specific classes which are connected to URI-patterns, meaning that accessing a matching URI will route the request to the attached class. To be more specific: 

Let's define a URI-pattern like this








