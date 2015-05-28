# 1. Basic Model
This is the basic Stupid Model, an extremely simple agent-based model used as a starting point for learning GAMA (or other ABM platforms).







## Formulation
  * The space is a two-dimensional grid of dimensions 100 x 100. The space is toroidal, meaning that if bugs move off one edge of the grid they appear on the opposite edge.

  * 100 bug agents are created. They have one behavior: moving to a randomly chosen grid location within +/- 4 cells of their current location, in both the X and Y directions. If there already is a bug at the location (including the moving bug itself—bugs are not allowed to stay at their current location unless none of the neighborhood cells are vacant), then another new location is chosen. This action is executed once per time step.

  * The bugs are displayed on the space. Bugs are drawn as red circles. The display is updated at the end of each time step.





## Model Definition

### the grid environment

We are going to defined a 100x100 grid toroidal environment.
First, we set the environment as torus by using the **torus** facet:

```
global torus: true{
}
```

Then, we define a grid with 100 rows and 100 columns and with a Von Neumann neighborhood:

```
grid cell width: 100 height: 100 neighbours: 4 {
}
```


### bug agent definition

Here we have to define the structure of the bug agents then their behaviour:
  * What is a bug agent?
    * A bug is by default situated in the space (located in a _cell_ called **my\_place**).

```
species bug {
	cell my_place;
```
  * It is represented by a circle shape of a red color which is defined using the **aspect** section.

```
species bug {
	aspect basic {
		draw circle(0.5) color: #red;
	}
}
```


  * What is the behavior of a bug?
    * It selects a destination cell or 'place' within a distance of 4 cells where there is no agent.
    * It stays at the same cell only if there is no neighbor place empty.

```
species bug {
	cell my_place;
	reflex basic_move {
		cell destination <- shuffle(my_place.neighbours4) first_with empty(each.agents);
		if (destination != nil) {
			my_place <- destination;
			location <- destination.location;
		}
	}
	...
}
```


The **`reflex`** within the **`species`** section declares the behavior of the bug. This **`reflex`** will be executed at each time step by the agent.

First, we declare the `destination` as a cell which is one of the empty neighbor place.

Then we check that the `destination` variable is not null and the agent moves. If `destination` is null (which means that all neighbors are already full), it stays where it is.

### instantiating bugs
  * How to instantiate the 100 bugs?
    * As we have no information they will be placed randomly by the system.
    * We introduce here the **`global`** section which is responsible to hold global variables and process global action.

```
global torus: true{
	init {
		create bug number: 100 {
			my_place <- one_of(cell);
			location <- my_place.location;
		}
	}
}
```

We add to the **`global`** section an **`init`** subsection where we call the **`create`** command. The **`init`** subsection will be executed upon the creation of the entity. Here the entity is the system itself, we call it the "world". Consequently, the bugs will be created before the start of the simulation and will be placed randomly on the default environment.

### display output
We are going to define in the experiment section a display output to display the environment in the user interface, listing species to display.
```
experiment stupidModel type: gui {
	output {
		display stupid_display {
			grid cell;
			species bug aspect: basic;
		}
	}
}
```

### Nota bene

In GAMA we cannot choose when to draw the agent thus the "The display is updated at the end of each time step." statement is of no interest (though it is the case).





## Complete Model

```
model StupidModel1

global torus: true{
	init {
		create bug number: 100 {
			my_place <- one_of(cell);
			location <- my_place.location;
		}
	}
}

grid cell width: 100 height: 100 neighbours: 4 {
	list<cell> neighbours4 <- self neighbours_at 4;
}

species bug {
	cell my_place;
	reflex basic_move {
		cell destination <- shuffle(my_place.neighbours4) first_with empty(each.agents);
		if (destination != nil) {
			my_place <- destination;
			location <- destination.location;
		}
	}
	aspect basic {
		draw circle(0.5) color: #red;
	}

}

experiment stupidModel type: gui {
	output {
		display stupid_display {
			grid cell;
			species bug aspect: basic;
		}
	}
}
```