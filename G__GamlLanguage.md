
# GAML



Models that users want to simulate in GAMA have to be written in a special language, called **GAML** (short for **GA**ma **M**odeling **L**anguage)

GAML is born from the necessity to have a high-level declarative way of defining and reusing structures found in almost all agent-based models. See [here](G__KeyConcepts) for more information about its background.

Although this choice requires users to learn a new programming (or better, _modeling_) language, everything has been made in GAMA to support a short learning curve, so that they can become almost autonomous in a limited time (informal measures taken at the different [events centered on GAMA](G__Events) have shown that one day is enough to acquire sufficient skills in writing complete models in GAML).

The documentation on GAML is organized in 5 main points:

  * Description of the general structure of a model: see [this page](G__OrganizationModel)
  * Description of the declaration of species (and all their components): see [this page](G__DefiningSpecies) and all its subpages
  * Description of the declaration of experiments: see [this page](G__DefiningExperiments) for regular experiments and [this one](G__BatchExperiments) for batch experiments.
  * Reference of the [language](G__GamlReference) regarding all the structures provided to modelers
  * Recipes of how to use special or advanced features offered in GAML: see this [page](G__Recipes).

In addition, some of the fundamental concepts behind GAML are also described in detail, both on the [modeling infrastructure](G__KeyConcepts) and the [runtime infrastructure](G__RuntimeConcepts) on which GAML is relying to run experiments on models.
