# creating a new project

Example: github

create new repository with .gitignore and readme

git clone https://github.com/evandor/skysail-notes.git

create new eclipse workspace

\(install bndtools\)

open bndtools perspective

new bnd osgi workspace

  create in: path of cloned repo 

  **osgi/workspace**

chmod 775 gradlew

./gradlew clean build

optional:

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

http://enroute.osgi.org/qs/200-workspace.html

