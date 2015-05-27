# Introduction

**This installation procedure does not work yet. Please refer to the installation on Eclipse Indigo:**
[installation de GAMA sous Eclipse Indigo](InstallProcedure15Juno.md)


# Details
  1. Download the Eclipse Modeling Tools version
    * http://www.eclipse.org/downloads/packages/eclipse-modeling-tools/junor
  1. Unpack it anywhere and run it
  1. Choose a new workspace
    * A workspace is a folder in which Eclipse stores all your projects (e.g /Users/username/Projects/Gama/MyWorkSpace).
  1. Install the required plugins. « Help » -> « Install new software »
    * In "Work with", choose "Juno - http://download.eclipse.org/releases/juno" and install:
      * In "Web, XML, Java EE and OSGI Entreprise Development"
        * Eclipse Web Developer Tools	3.4.0.v201203141800
        * Eclipse XML Editors and Tools 3.4.0.v201111021744
      * In "Collaboration"
        * Subversive SVN JDT Ignore Extensions (Optional) 1.0.0.I20120601-1700
        * Subversive SVN Team Provider 1.0.0.I20120601-1700 (this one will ask, once restarted, to download one or more connectors. Choose the latest SVNKit — 1.3.7)
    * In "work with", write "http://download.eclipse.org/modeling/tmf/xtext/updates/composite/releases/", click on "Add" and choose a name (e.g. Xtext)
      * In "Xtext-2.3.0"
        * Xtext SDK	2.3.0.v201206120633
        * Xtend SDK	2.3.0.v201206120633
  1. Eclipse proposes to restart -> Restart now
  1. Add SVN repository exploring perspective
    * To activate this perspective, choose Window / Open Perspective / Other... and select "SVN Repository Exploring"
    * A popup appears (Discovery of SVN connector)
    * Choose: SVN Kit 1.3.7
      * Popup Unsigned content -> ok
    * Popup -> restart now
  1. New > repository location
    * https://gama-platform.googlecode.com/svn
    * Finish (& wait)
  1. Checkout of the GAMA code source
    * In the SVN repository view, navigate to the directory "branches/GAMA\_CURRENT" and select "Find/Checkout As..." from the contectual menu.
    * Choose "Find projects in the children of the selected resource" and follow the indications.
    * Pop-up "Check Out projects", all projects should be selected. Finish.
    * Once the checkout is finished, switch to Java Perspective.

  * N.B: For people used to use svn from a terminal step 6 to 8 can be replace by:
    * Checkout the code from a terminal.
```
$ mkdir Projects/Gama/Sources
$ svn checkout https://gama-platform.googlecode.com/svn/branches/GAMA_CURRENT/
```
    * Link the source with eclipse
      * File > Import > General > Existing Projects into Workspace
      * Select root directory of Gama Sources (e.g Projects/Gama/Sources/GAMA\_CURRENT) and import each project one by one.

To compile and run GAMA properly, you will need to configure your Eclipse IDE and the GAMA `.product` file.
  1. By default, Eclipse uses the Java 7 whereas GAMA needs Java 6. We have thus to change the version of the Java compiler.
    * Window->Preferences
    * In: Java / Compiler: set "Compiler compliance level" to 1.6
    * In: Java / Installed JREs -> Add -> Standard VM -> JRE home -> Directory and choose the directory of a Java 6 jre
      * Download of the JRE Java 6: http://www.oracle.com/technetwork/java/javase/downloads/jre-6u31-download-1501637.html
    * In: Java / Installed JREs -> select the Java 1.6
  1. You should configure the GAMA `.product` file depending on your OS.
    * In the `msi.gama.application` project, open the `gama1.5.product` file
    * In: the "Dependencies" tab: click on "Add Required plug-ins"
    * In: the "Launching" tab: check whether the launching options are correct
      * In particular, for a 32bits OS, you have to change in "VM Arguments" "-Xmx1536m" into "-Xmx1024m"
      * For 64bits OS, check that the option "-d32" is not in the "VM Arguments" (otherwise delete it) in the "macosx" specific tab.
  1. Compile and Run GAMA
    * Do a "Project -> Clean... (clean all projects)"
    * In `gama1.5.product` file, in "Overview" tab.
      * click on the « Synchronize » link. This will ensure your product has updated the inclusion of the plugins (from both Eclipse 3.7 and the new XText). Do not forget to save it.
      * click on the « Launch an Eclipse application » link. Note that, a run configuration will be automatically created allowing to only click on the run button for future runs.

Have fun!