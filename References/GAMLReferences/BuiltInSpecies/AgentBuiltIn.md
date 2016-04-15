
# The 'agent' built-in species (Under Construction)


As described in the [presentation of GAML](https://github.com/mazarsju/gama_doc_17/wiki/Tutorials/LearnGAMLStepByStep/Introduction.md), the hierarchy of species derives from a single built-in species called `agent`. All its components (attributes, actions) will then be inherited by all direct or indirect children species (including [`model`](https://github.com/mazarsju/gama_doc_17/wiki/References/GAMLReferences/BuiltInSpecies/ModelBuiltIn.md) and [`experiment`](https://github.com/mazarsju/gama_doc_17/wiki/References/GAMLReferences/BuiltInSpecies/ExperimentBuiltIn.md)), with the exception of species that explicitly mention `use_minimal_agents: true` as a facet, which inherit from a stripped-down version of `agent` (see below).



## `agent` attributes
`agent` defines several attributes, which form the minimal set of knowledge any agent will have in a model.
  * 


## `agent` actions