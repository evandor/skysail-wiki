# Eclipse

These instructions are for Eclipse Oxygen, but should apply to older versions as well.

* Download Eclipse \([Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/oxygenr)\) or use the installer.
* Launch Eclipse using a new workspace
* Using the Marketplace, search for "bndtools" and install the latest version \(e.g. Bndtools 3.3.0 REL\)
* Using the Marketplace, search for "scala" and install the latest version \(e.g. Scala IDE 4.2.x\)
* clone the [skysail-core](https://github.com/evandor/skysail-core) repository \(command line or using eclipse's Git perspective\)
* Import all projects but the uppermost \(the skysail-core parent folder\) from that repository
* You can close the project "io.skysail.bundled", this is only used to create bundles from ordinary jars.
* Clean and Build all projects; if there are errors, click on "Bndtools &gt; Refresh Repositories" in the bndools perspective.
* open skysail.core/core.test.bndrun and start it by clicking "Run OSGi" \(upper right of the Run-Tab-Editor\)



