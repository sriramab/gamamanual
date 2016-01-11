
# Attaching Skills and Control




GAMA allows to attach skills and a control architecture to agents through the facets **skills** and **control**.

Skills are built-in modules that provide a set of related built-in variables and built-in actions (in addition to those already provided by GAMA) to the species that declare them.

Control are agent control architectures that can be used in addition to the [common behavior structure](G__DefiningBehaviors).


## Table of contents 

* [Attaching Skills and Control](#attaching-skills-and-control)
	* [Skills](#skills)
	* [Control Architecture](#control-architecture)





## Skills

A declaration of skill is done by filling the skills facet in the species definition:

```
species my_species skills: [skill1, skill2] {
    ...
}
```

Skills have been designed to be mutually compatible so that any combination of them will result in a functional species. The list of available skills in GAMA is:
* moving: for agents that need to move.

So, for instance, if a species is declared as:

```
species foo skills: [moving]{
...
}
```

its agents will automatically be provided with the following variables : "speed, heading, destination (r/o)" and the following actions: "move, goto, wander, follow" in addition to those built-in in species and declared by the modeller. Most of these variables, except the ones marked read-only, can be customized and modified like normal variables by the modeller. For instance, one could want to set a maximum for the speed; this would be done by redeclaring it like this:

```
float speed max:100 min:0;
```

Or, to obtain a speed increasing at each simulation step:

```
float speed max:100 min:0  <- 1 update: speed * 1.01;
```

Or, to change the speed in a behavior:

```
if speed = 5 {
    speed <- 10;
}
```

A complete description of existing skills is available [here](G__BuiltInSkills).





## Control Architecture

GAMA integrates several agent control architectures that can be used in addition to the common behavior structure:
* weighted\_tasks
* sorted\_tasks
* probabilistic\_tasks
* fsm
* user\_only
* user\_first
* user\_last

The choice of an architecture (that is optional) is made through the **control** facet:
```
species ant control: fsm {
   ...
}
```

A description of all existing control architectures is available [here](G__BuiltInControlArchitectures).