
# Regular Species (Under contruction)

Regular species are composed of attributes, actions, reflex, aspect etc... They will describe the behaviour of our agents. You can instantiate as much as you want agents from a regular species. And you can define as much as you want different regular species.

## Table of contents 

* [Regular Species (Under contruction)](#regular-species-(under-construction))
	* [Declaration](#declaration)
	* [Actions](#actions)
		* [die](#die)
		* [debug](#debug)
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

## Actions

Some actions are define by default for a minimal agent.

### Die

To kill the current occurrence of a species, the key world is ```die```. As it is an action, you have to put the keyworld ```do``` just before : 

```
species MySpecies{
    reflex SelfKill {
        do die;
    }
}
```

### Debug

Some other actions can be useful for debugging your species, such as ```debug``` (will write in the console the properties of your agent).
```
species MySpecies{
    reflex PrintDebug {
        do debug;
    }
}
```

### Write

The ```write``` action can be very useful also. It will write a text in the console. This action takes one argument, it is overloaded for almost every type you want. It can be used with 2 syntax : as a normal action with the keyworld ```do``` or simply with the keyworld ```write``` :
```
species MySpecies{
    int simpleType <- 5;
    list complexeType <- [3.5,"string"];
    reflex WriteMessage {
        do write(simpleType); // <-- call the write action as a normal action
        write(complexeType);  // <-- use the simple special writing for the write action
    }
}
```

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

See how to [schedule agents](G__RuntimeConcepts#scheduling-of-agents).

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