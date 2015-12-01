# Architecture of GAMA



GAMA is made of a number of Eclipse Java projects, some representing the core projects without which the platform cannot be run, others additional plugins adding functionalities or concepts to the platform.

__Vocabulary:__
Each project is either designed as a __plugin__ (containing an xml file "plugin.xml") or as a __feature__ (containing an xml file "feature.xml").
  * A __plugin__ can be seen as a module (or bundle in the OSGI architecture), which can be necessary (the GAMA platform can't run without it) or optional (providing new functionalities to the platform). This decomposition between several plugins ensure the cohesion between functional blocks, each plugin has to be as independent as he can.
  * A __feature__ is a group of one or several modules (or plugin), which can be loaded. NB : Unlike a plugin, a feature does not include source code, but only two files : a build.properties and a feature.xml.
To see how to create a plugin and a feature, please read this page [link to G__InstallingGitVersion].

  * `msi.gama.application` essentialy described the graphical user interface (`msi.gama.gui` package), which contains the following sub-packages :
    * `msi.gama.gui.displays`
    * `msi.gama.gui.navigator`
    * `msi.gama.gui.parameters`
    * `msi.gama.gui.svn`
    * `msi.gama.gui.swt`
    * `msi.gama.gui.views`
    * `msi.gama.gui.wizards`
  * `msi.gama.core` encapsulates the core of the modeling and simulation facilities offered by the platform : runtime, simulation, meta-model, data structures, simulation kernel, scheduling, etc. It contains 2 main packages :
    * `msi.gama`
    * `msi.gaml`, which defines the GAML modeling language: keywords, operators, statements, species, skills, and so on.
  * `msi.gama.ext` gathers all the external libraries upon which GAMA relies ;
  * `msi.gama.lang.gaml` contains the `gaml.xtext` file which defines the GAML grammar ;
  * `msi.gama.lang.gaml.ui` contains the GAML Editor (syntax highlighting, code completion, ...)
  * `msi.gama.processor` is responsible for processing the annotations made in the Java source code and producing **additions** to GAML (Java, properties and documentation files), which are added into a source package called "gaml.additions" (containing two main generated files: `GamlAdditions.java` and `GamlDocumentation.java`). These additions are loaded automatically when GAMA launches, allowing extensions made by developers in other plugins to be recognized when their plugin is added to the platform.