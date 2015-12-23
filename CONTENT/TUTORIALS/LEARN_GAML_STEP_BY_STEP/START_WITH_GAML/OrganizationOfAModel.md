[//]: # (Subsection:START_WITH_GAML)
[//]: # (Previous:null)
[//]: # (Next:BasicProgramingConceptsInGAML)
[//]: # (Prerequisite:[])


# Organization of a model

As already extensively detailed in the [key concepts page](G__KeyConcepts), defining a model in GAML amounts to defining a _model species_, which later allows to instantiate a _model agent_ (aka a _simulation_), which may or may not contain micro-species, and which can be flanked by _experiment plans_ in order to be simulated.

This conceptual structure is respected in the definition of model files, which follows a similar pattern:

1. Definition of the _global species_, preceded by a _header_, in order to represent the _model species_
1. Definition of the different micro-species (either nested inside the _global species_ or at the same level)
1. Definition of the different _experiment plans_ that target this model


## Table of contents 

* [Organization of a model](#organization-of-a-model-under-construction)
	* [Model Header (model species)](#model-header-model-species)
	* [Species declarations](#species-declarations)
	* [Experiment declarations](#experiment-declarations)



## Model Header (_model species_)

The header of a model file begins mandatorily with the declaration of the name of the model. Contrarily to other statements, this declaration **does not** end with a semi-colon.
```
model name_of_the_model
```
The name of the model is not necessarily the same as the name of the file. It must conform to the general rule for naming species, i.e. be a valid identifier (beginning with a letter, containing only letters, digits and dashes). This name will be used for building the name of the model species, from which _simulations_ will be instantiated. For instance, the following declaration:
```
model dummy
```
will internally create a species called `dummy_model`, child of the abstract species `model`, from which simulations (called `dummy_model0`, `dummy_model1`, etc.) will be instantiated.

This declaration is followed by optional import statements that indicate which other models this model is importing. Import statements **do not** end with a semi-colon.

Importing a model can take two forms. The first one, called _inheritance import_, is declared as follows:
```
import "relative_path_to_a_model_file"
import "relative_path_to_another_model_file"
```
The second one, called _usage import_, is declared as follows:
```
import "relative_path_to_a_model_file" as model_identifier
```
When importing models using the first form, all the declarations of the model(s) imported will be merged with those of the current model (in the order with which the import statements are declared, i.e. the latest definitions of global attributes or behaviors superseding the previous ones).
The second form is reserved for using models as _micro-models_ of the current model. This possibility is still experimental in the current version of GAMA.

The last part of the _header_ is the definition of the `global` species, which is the actual definition of the _model species_ itself.
```
global {
    // Definition of global attributes, actions and behaviors
}
```

Note that neither the imports nor the definition of `global` are mandatory. Only the `model` statement is.



## Species declarations

The header is followed by the declaration of the different species of agents that populate the model. Note that the possibility to define the species _after_ the `global` definition is actually a convenience: these species are micro-species of the model species and, hence, could be perfectly defined as nested species of `global`. For instance:
```
global {
    // definition of global attributes, actions, behaviors
}

species A {…}

species B {…}
```
is completely equivalent to:
```
global {
    // definition of global attributes, actions, behaviors

    species A {…}

    species B {…}
}
```


## Experiment declarations

Experiments are usually declared at the end of the file. They start with the keyword "experiment". They contains the simulation parameters, and the definition of the output. You can declare as much experiment as you want.

```
experiment first_experiment {
    // definition of parameters

    // definition of output
    output {...}
}

experiment second_experiment {
    // definition of parameters

    // definition of output
}
```
