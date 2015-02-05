# Tutorial - Create a new skysail application

This tutorial assumes that you have set up Eclipse and gradle. 

## 1. Create a new bndtools project

...

## 2. Setup the cnf folder

In build.bnd:

    javac.source:          1.8
    javac.target:          1.8


Add

    	aQute.bnd.deployer.repository.FixedIndexedRepo; name=Skysail Hub;           locations=https://github.com/evandor/skysail/raw/master/cnf/releaserepo/index.xml,\
        aQute.bnd.deployer.repository.FixedIndexedRepo; name=Skysail Framework Hub; locations=https://github.com/evandor/skysail-framework/raw/master/cnf/releaserepo/index.xml,\
        aQute.bnd.deployer.repository.FixedIndexedRepo; name=Skysail Repository;    locations=https://github.com/evandor/skysail-repository/raw/master/index.xml.gz,\

to ext/repositories (and make sure to keep the line endings properly).

## 3. Create a build file in your new project

build.gradle:

```
sourceSets {
    generated {
        java {
            srcDirs = ['src-gen']
        }
    }
}

task runApt(type: JavaCompile, group: 'build', description: 'Generates the apt sources') {
    source = sourceSets.main.java
    classpath = configurations.compile// + configurations.querydslapt
    options.compilerArgs = [
            "-proc:only",
            "-processor", "de.twenty11.skysail.server.ext.apt.processors.ApplicationProcessor"
    ]
    destinationDir = sourceSets.generated.java.srcDirs.iterator().next()
}

compileJava {
    dependsOn runApt
    source runApt.destinationDir
}

compileGeneratedJava {
    dependsOn runApt
    options.warnings = false
    classpath += sourceSets.main.runtimeClasspath
}

clean {
    delete sourceSets.generated.java.srcDirs
}
```


