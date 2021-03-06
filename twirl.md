# Twirl

Idea: Use twirl for server side template rendering.

Problems

* Compiling templates -&gt; use gradle-twirl-plugin
* OSGi classloading -&gt; export generated html templates
* Combining templates from different bundles

### Activate html templates in bundle:

in bnd.bnd:

add

```
-buildpath: \
...
io.skysail.bundled.twirl-api_2.11;version=1.3,\
io.skysail.bundled.twirl-parser_2.11;version=1.3,\
io.skysail.bundled.twirl-compiler_2.11;version=1.3,\
org.scala-lang.scala-compiler;version=2.11

...

Export-Package: io.skysail.<package>.html

```

In build.gradle

```
buildscript {
    repositories {
        maven {
            url 'https://plugins.gradle.org/m2/'
        }
    }
    dependencies {
        ...
        classpath "gradle.plugin.io.skysail.gradle:twirlosgi-gradle-plugin:0.1.1"
    }
}

...
apply plugin: 'io.skysail.twirl.osgi'
 
```





