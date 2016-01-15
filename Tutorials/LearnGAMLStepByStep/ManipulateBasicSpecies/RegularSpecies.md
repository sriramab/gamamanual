# Regular species

Regular species are composed of attributes, actions, reflex, aspect etc... They describes the behaviour of our agents. You can instantiate as much as you want agents from a regular species, and you can define as much as you want different regular species. You can see a species as a "class" in OOP.

## Index

* [Declaration](#declaration)
* [Built-in Attributes](#built-in-attributes)
* [Built-in Actions](#built-in-actions)
* [The init statement](#the-init-statement)
* [The aspect statement](#the-aspect-statement)
* [Instantiate an agent](#instantiate-an-agent)

## Declaration

The regular species declaration starts with the keyword `species` followed by the name (or followed by the facet `name:`) :

```
species my_specie {
}
```

or:

```
species name:my_specie {
}
```

Directly in the "species" scope, you have to declare all your attributes (or "member" in OOP). You declare them exactly the way you declare basic variables. Those attributes are accessible wherever you want inside the species scope.

```
species my_specie {
	int variableA;
}
```

## Built-in attributes

As for the global species, some attributes exist already by default in a regular species. Here is the list of built-in attributes:

* **name** (type: string) is used to name your agent. By default, the name is equal to the name of your species + an incremental number. This name is the one visible on the species inspector.
* **location** (type: point) is used to control the position of your agent. 
* **shape** (type: geometry) is used to describe the geometry of your agent. If you want to use some intersection operator between agents for instance, it is this geometry that is computed (nb : it can be totally different from the aspect you want to display for your agent !). By default, the shape is a point.
* **host** (type: agent) is used when your agent is part of another agent. We will see this concept a bit further, in the topic multi-level architecture (TODO_URL).

All those 4 built-in attributes can be accessed in both reading and writing very easily:

```
species my_species {
	init {
		name <- "custom_name";
		location <- {0,1};
		shape <- rectangle(5,1);
	}
}
```

All those built-in attributes are attributes of an agent (an instantiation of a species). Species has also their own attributes, which can be accessed with the following syntax (read only) :

```
name_of_your_species.attribute_you_want
```

Here is the list of those attributes:

* **name** (type: string) returns the name of your species
* **attributes** (type: list of string) returns the list of the names of the attributes of your species
* **population** (type: list) returns the list of agent that belong to it 
* **subspecies** (type: list of string) returns the list of species that inherit directly from this species (we will talk about the concept of [inheritance](Inheritance) later)
* **parent** (type: species) returns its parent species if it belongs to the model, or `nil` otherwise (we will talk about the concept of [inheritance](Inheritance) later)

## Built-in action

Some actions are define by default for a minimal agent. We already saw quickly the action write, used to display a message in the console.
Another very useful built-in action is the action die, used to destroy an agent.

```
species my_species{
    reflex being_killed {
        do die;
    }
}
```

Here is the list of the other built-in actions which you can find in the documentation: (TODO_URL) debug, message, tell.

## The init statement

After declaring all the attributes of your species, you can define an initial state (before launching the simulation). It can be seen as the "constructor of the class" in OOP.

```
species my_species {
	int variableA;
	init {
		variableA <- 5;
	}
}
```

## The aspect statement

Inside each species, you can define one or several aspects. This scope allows you to define how you want your species to be represented in the simulation.
Each aspect has a special name (so that they can be called from the experiment). Once again, you can name your aspect by using the facet `name:`, or simply by naming it just after the `aspect` keyword.

```
species my_species {
	aspect standard_aspect { // or "aspect name:standard_aspect"
	}
}
```

You can then define your aspect by using the statement `draw`. You can then choose a geometry for your aspect (facet `geometry`), a color (facet `color`), an image (facet `image`), a text (facet `text`)... We invite you to read the documentation about the draw statement to know more about.

```
species name:my_species {
	aspect name:standard_aspect {
		draw geometry:circle(1) color:#blue;
	}
}
```

In the experiment scope, you have to tell the program to display a particular species with a particular aspect (nb : you can also choose to display your species with several aspect in the same display). 

```
experiment my_experiment type:gui
{
	output{
		display my_display {
			species my_species aspect:standard_aspect;
		}
	}
}
```

Now there is only one thing missing to display our agent: we have to instantiate them.

## Instantiate an agent

As already said quickly in the last session, the instantiation of the agents is most often in the init scope of the global species (this is not mandatory of course. You can instantiate your agents from an action / behavior of any specie). Use the statement create to instantiate an agent. 
The facet species is used to specify which species you want to instantiate. 
The facet number is used to tell how many instantiation you want. 
The facet with is used to specify some default values for some attributes of your instance. For example, you can specify the location.

```
global{
	init{
		create species:my_species number:1 with:(location:{0,0},vA:8);
	}
}


species name:my_specie {
	int vA;
}
```

Here is an example of model that display an agent with a circle aspect in the center of the environment:

```
model display_one_agent

global{
	float worldDimension <- 50#m;
	geometry shape <- square(worldDimension);
	init{
		point center <- {(worldDimension/2),(worldDimension/2)};
		create species:my_species number:1 with:(location:center);
	}
}

species name:my_species {
	aspect name:standard_aspect {
		draw geometry:circle(1#m);
	}
}

experiment my_experiment type:gui
{
	output{
		display myDisplay {
			species my_species aspect:standard_aspect;
		}
	}
}
```