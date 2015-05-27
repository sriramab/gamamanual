# Architecture of GAMA

---

GAMA is made of a number of Eclipse Java projects, some representing the core projects without which the platform cannot be run, others additional plugins adding functionalities or concepts to the platform.

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