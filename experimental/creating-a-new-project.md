# creating a new workspace

Example: github

* create new repository with .gitignore and readme
* git clone [https://github.com/evandor/skysail-notes.git](https://github.com/evandor/skysail-notes.git)
* create new eclipse workspace \(with same name\)
* \(install bndtools if note done yet\)
* open bndtools perspective
* new bnd osgi workspace  
  create in: path of cloned repo
  **osgi/workspace**
* chmod 775 gradlew
* ./gradlew clean build
* optional:
  create test project

scala:

set root .gitignore to

```
*.class
*.log

# sbt specific
.cache
.history
.lib/
dist/*
target/
lib_managed/
src_managed/
project/boot/
project/plugins/project/

# Scala-IDE specific
.scala_dependencies
.worksheet

.gradle/
/generated/
.metadata
```

links:

[http://enroute.osgi.org/qs/200-workspace.html](http://enroute.osgi.org/qs/200-workspace.html)

[https://github.com/bndtools/bnd/blob/master/biz.aQute.bnd.gradle/README.md\#gradle-plugin-for-workspace-builds](https://github.com/bndtools/bnd/blob/master/biz.aQute.bnd.gradle/README.md#gradle-plugin-for-workspace-builds)

