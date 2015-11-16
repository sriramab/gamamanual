
# Regular Species

Regular species are composed of attributes, actions, reflex, aspect etc... They will describe the behaviour of our agents. You can instantiate as much as you want agents from a regular species. And you can define as much as you want different regular species.

## Table of contents 

* [Regular Species](#regular-species)
	* [Declaration](#declaration)
	* [Facets](#facets)
		* [skills](#skills)
		* [frequency](#frequency)
		* [control](#control)
		* [parent](#parent)
		* [schedules](#schedules)
		* [mirror](#mirror)
	* [Aspect](#aspect)

## Declaration
A GAMA model can contain one or several regular species. The regular species declaration starts with the keyword ```species``` followed by the name (or followed by the facet ```name:````) :

```
species mySpecies {
}
```
or :
```
species name:mySpecies {
}
```
As for all the other species, you can declare attributes, actions, behaviours, reflex, init, aspects... for the species.

## Facets

### Skills

You can define a list of skills for a species. Defining a skill for your species will allow you to use a bunch of new actions.

```
species mySpeciesWithUsefullSkills skills: [moving,otherSkill] {
    reflex walk {
        do wander(amplitude:90) // <- "wander" is an action from the skill "moving".
    }
}
```

### Frequency

The frequency is an int used to define the execution frequency of the species (default value: 1). For instance, if frequency is set to 10, the population of agents will be executed only every 10 cycles.

```
species mySpecies frequency:10 {
}
```

### Control

TODO

### Parent

TODO

### Schedules

TODO

### Mirror

See the [mirror species](G__MirrorSpecies).

## Aspect

For each species, you can define one or several aspects. In the ```experiment``` session, you just have to choose the aspect you want for you species.

```
species MySpecies {
    aspect MyFirstAspect {
        draw circle(1);
    }
    aspect MySecondAspect {
        draw square(1);
    }
}

experiment MyExp type: gui {
    output {
        display MyDisplay type: opengl {
            species MySpecies aspect:MyFirstAspect;
        }
    }
}
```
