# Setup your IDE

Using the skysail framework or creating skysail applications do not require a specific IDE or build environment. Still, in order to keep things simple (well, yes, for ourselves) we'll explain how to setup skysail with Eclipse only.

## Eclipse

### Download

Go to [eclipse.org](http://www.eclipse.org), click the download link and search for the "Eclipse IDE for Java Developers" edition for your platform. Download and follow the instructions. 

### Workspace and initial plugins

Create a new workspace (yes, new!).

Start the eclipse marketplace (in the Help menu) and search for "bndtools". Install the Bndtools 2.4.0.REL (or greater) version from "Neil Bartlett and others".

Restart.

### Lombok

skysail uses [lombok](http://www.projectlombok.org) to reduce some of the typical java boilerplate code. Though you don't need lombok to write skysail plugins, if you want to compile the skysail framework code, you'll have to install it.
