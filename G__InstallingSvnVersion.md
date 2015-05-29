# Installing the SVN version

This installation procedure has been tested on MacOS X 10.10 (Yosemite) and Windows 8. On MacOS x 10.10 (Yosemite), please have a look here: [install Java on Yosemite](G__Installation) for details about the Java version to use. 

**Notice that GAMA is in a migration phase from Eclipse 3.8.2 to Eclipe Luna 4.4.2, and from SVN to Git. Other previous Eclipse versions are not supported anymore**.

**Important note: the current SVN version is no more compatible with the GAMA 1.6.1 release.**
  * If you plan to create plugin that should be compatible with the release, please download the GAMA code source at revision r11988 (on Google Code) and [Eclipse following this procedure](G__InstallingSvnOldVersions)


## Detailed Instructions for Eclipse 4.4.2 (Luna SR2)
### Get and configure Eclipse Luna
1. Download the Eclipse Modeling Tools version of Luna SR2
  * https://eclipse.org/downloads/packages/eclipse-modeling-tools/lunasr2
2. Unpack it anywhere and run it
3. Choose a new workspace
  * A workspace is a folder in which Eclipse stores all your projects.
4. Install the required plugins. « Help » -> « Install new software »
  * In "work with", write "http://download.eclipse.org/modeling/tmf/xtext/updates/composite/releases/", click on "Add" and choose a name (e.g. Xtext)
    * In "Xtext", install the following one:
      * Xtext Complete SDK	2.8.2.v201504100559

### Get code source from GitHub
In Eclipse:
1. Windows > Open Perspective > Other…
  * Git
2. Click on "Clone a Git repository"
  * First window:
    * URI: https://github.com/gama-platform/gama.git
  * Branch Selection:
    * Check master
    * Next
  * Local Destination
    * Choose a Directory
    * Finish

You have then to import projects:
1. Right-Click on Working Directory > Import projects
  * Select a wizard to use for importing projects:
    * "Import existing projects" should be  checked
    * "Working Directory" should be selected
    * Next
  * In Import Projects:
    * Uncheck « Search for nested project »
    * Check the projects you want to import
    * Finish

Go back to the Java perspective
