
# GAML



Models that users want to simulate in GAMA have to be written in a special language, called **GAML** (short for **GA**ma **M**odeling **L**anguage)

GAML is born from the necessity to have a high-level declarative way of defining and reusing structures found in almost all agent-based models. See [here](https://github.com/mazarsju/gama_doc_17/wiki/Tutorials/LearnGAMLStepByStep/Introduction.md) for more information about its background.

Although this choice requires users to learn a new programming (or better, _modeling_) language, everything has been made in GAMA to support a short learning curve, so that they can become almost autonomous in a limited time (informal measures taken at the different [events centered on GAMA](https://github.com/mazarsju/gama_doc_17/wiki/WikiOnly/Events.md) have shown that one day is enough to acquire sufficient skills in writing complete models in GAML).

The documentation on GAML is organized in 5 main points:

  * Description of the general structure of a model: see [this page](https://github.com/mazarsju/gama_doc_17/wiki/Tutorials/LearnGAMLStepByStep/StartWithGAML/ModelOrganization.md)
  * Description of the declaration of species (and all their components): see [this page](https://github.com/mazarsju/gama_doc_17/wiki/Tutorials/LearnGAMLStepByStep/ManipulateBasicSpecies.md) and all its subpages
  * Description of the declaration of experiments: see [this page](https://github.com/mazarsju/gama_doc_17/wiki/Tutorials/LearnGAMLStepByStep/DefiningGUIExperiment.md) for regular experiments and [this one](https://github.com/mazarsju/gama_doc_17/wiki/Tutorials/LearnGAMLStepByStep/ExploringModels/BatchExperiments.md) for batch experiments.
  * Reference of the [language](https://github.com/mazarsju/gama_doc_17/wiki/References/GamlReference.md) regarding all the structures provided to modelers
  * Recipes of how to use special or advanced features offered in GAML: see this [page](https://github.com/mazarsju/gama_doc_17/wiki/Tutorials/Recipes.md).

In addition, some of the fundamental concepts behind GAML are also described in detail, both on the [modeling infrastructure](https://github.com/mazarsju/gama_doc_17/wiki/Tutorials/LearnGAMLStepByStep/Introduction.md) and the [runtime infrastructure](https://github.com/mazarsju/gama_doc_17/wiki/Tutorials/LearnGAMLStepByStep/OptimizingModels/RuntimeConcepts.md) on which GAML is relying to run experiments on models.