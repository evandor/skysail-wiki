# IntelliJ

These instructions are for IntelliJ IDEA 2017.1, but should apply to older versions as well.

* Download [IDEA](https://www.jetbrains.com/idea/). Unfortunately you'll need the commercial edition, the Community Edition will not work 
* Make sure the _scala_ and _Osmorc_ plugins are enabled and set up
* clone the [skysail-core](https://github.com/evandor/skysail-core) repository \(command line or using IDEA\)
* Import the project \(navigating to the repository root\) and choose import from external model "bnd/Bndtools".
* You will see an "Unlinked gradle project?" message - make sure to add Gradle support with these settings: 
* * Use auto-import
  * deselect "create separate module per source set"
  * Use gradle wrapper task configuration
* Refresh all projects in the gradle view
* right-click skysail.core/core.test.bndrun and select "Create 'skysail.core'" \(bnd\)
* start the the runtime configuration.





