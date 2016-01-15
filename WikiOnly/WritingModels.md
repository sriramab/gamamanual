# Writing Models



Models in GAMA play the same role as classes in Java or C++: they represent both the knowledge about a particular phenomenon a user wants to simulate and the way(s) to simulate it. A model is nothing more than a text file (or a collection of text files that refer to each other), which contains instructions in a [specific language](https://github.com/gama-platform/gama/wiki/Content\WikiOnly\GamlLanguage.md) called GAML (for "GAMA Modeling Language").
A model can then be theoretically edited using any text processor and later loaded into GAMA to [run experiments](https://github.com/gama-platform/gama/wiki/Content\References\PlatformDocumentation\RunningExperiments.md). However, because of the richness of the language, using a dedicated tool (with online help, live validation) is clearly the best way to write correct models.

The GUI version of GAMA offers such an _integrated model development environment_, which is composed of a set of coupled tools to support modelers in the [edition](https://github.com/gama-platform/gama/wiki/Content\References\PlatformDocumentation\EditingModels.md), [validation](https://github.com/gama-platform/gama/wiki/Content\References\PlatformDocumentation\EditingModels\ValidationOfModels.md), and [management](https://github.com/gama-platform/gama/wiki/Content\References\PlatformDocumentation\WorkspaceProjectsAndModels.md) of models. An optional [graphical modeling editor](G__GraphicalEditor) can also be installed on top of these tools to support higher-level modeling activities (similar to what a UML editor with Java bindings may provide to a Java development environment).

This chapter contains a description of these different tools and a comprehensive guide to the [GAML language](https://github.com/gama-platform/gama/wiki/Content\WikiOnly\GamlLanguage.md), including a [complete reference](https://github.com/gama-platform/gama/wiki/Content\References\GamlReference.md) of all the built-in structures and facilities offered in its current version.

Please proceed to one of these sections :

  * 1. [Editing Models](https://github.com/gama-platform/gama/wiki/Content\References\PlatformDocumentation\EditingModels.md)
  * 2. [GAML Language](https://github.com/gama-platform/gama/wiki/Content\WikiOnly\GamlLanguage.md)
  * 3. [GAML Reference](https://github.com/gama-platform/gama/wiki/Content\References\GamlReference.md)
  * 4. [Optimizing Models](https://github.com/gama-platform/gama/wiki/Content\Tutorials\LearnGAMLStepByStep\OptimizingModels\OptimizingModels.md)