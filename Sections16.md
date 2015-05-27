
<br />
# Foreword
The structure of a model is composed of a header, followed by the declaration of several species of agents. Among these species, some play a special role: the `global` species defines the attributes and behaviors of the agent that _represents_ the model (called the [`world`](Keywords16#world.md) in GAML, and equivalent to the global context of the model), the different [`experiment`](Experiments16.md) species allow to define agents that can execute the model, and the others (i.e. [`species`](Species16.md) or `grid`) the agents that populate the model.
<br />
All these species follow the same definition pattern and only accept sub-statements that represent the declarations of their [attributes](Variables16.md), [actions](ActionGAMA16.md), [behaviors](Behaviors16.md) and [aspects](Aspect16.md). In addition, experiment species allow to declare [parameters](output16#Parameters.md), exploration [methods](batch16#Batch-Methods.md) and [outputs](output16#Output.md).

Example of a simple model:

http://gama-platform.googlecode.com/files/simple_model_example.PNG

# Header
The header of a model must define the name of the model (which can be different from the name of the file):
```
model my_first_model
```

It can optionally import other model files, which contents will be included as if they were defined in the importing file (in the order they are provided). The path to these files must be relative to the location of the importing file.
```
import "../include/schelling_common.gaml"
import "../include/data_global.gaml"
```


# <font color='blue'>Global species</font>

The "global" species defines the attributes, actions and behaviors that describe the world agent. This species automatically inherits from a number of built-in attributes and actions (see [global built-in variables](Keywords16.md)). All the attributes defined here can be refered by agents of other species or other places in the model code. The behaviors described in this species will be executed first at each step of a simulation.
Example:

```
global {
	int numberBugs <- 100;
	float globalMaxConsumption <- 1;
	float globalMaxFoodProdRate <- 0.01;
	init {
		create bug number: numberBugs;
	}
}
```

The attribute `shape` of the global species allows to define the global environment. GAMA supports three types of topologies for environments: continuous, grid and graph. By default, the world agent has a continuous topology and its geometry is a rectangle of size 100mx100m. The size of the rectangle can be defined:
  * using a geometry: `geometry shape <- rectangle(300,100);`
  * using a shapefile (GIS): envelope of all the data contained in the shapefile: `geometry shape <- envelope("bounds.shp");`,
    * a raster file (asc): `geometry shape <- envelope("bounds.asc");`,

Example:

```
global {
	float number_of_cars <- 1000;
	file road_shapefile <- file("../includes/roads.shp");
	geometry shape <- envelope(road_shapefile);
        init {
		create car number: number_of_cars ;
	}
}
```
# <font color='blue'>Species and grids</font>

All the species that define the agents belonging to the model can be written directly after `global`. For the sake of clarity, they can also be enclosed inside a statement called `entities`, which is not mandatory.
Example:

```
entities {
	species bug  {
		float evol <- 1;
		rgb color <- rgb ([255, 255/evol, 255/evol]);
		float maxConsumption <- globalMaxConsumption;
		stupid_cell myPlace update: location as stupid_grid;
		reflex basic_move {
			stupid_cell destination <- one_of ((myPlace neighbours_at 4) where empty(each.agents));
			if  destination != nil {
				location <- destination;
			}
		}
		reflex grow {
			float transfer <- min ([maxConsumption, myPlace.food]);
			evol <- evol + transfer;
			myPlace.food <- myPlace.food - transfer;
		}
		aspect basic {
			draw circle(1) color: color;
		}
	}
}
```

This section can also include the definition of one or several species that define a [grid topology](Grid16.md). Example:

```
entities {
   grid stupid_cell width: 100 height: 100 torus: false {
      rgb color <- rgb('black');
      float maxFoodProdRate <- globalMaxFoodProdRate;
      float maxConsumption <- globalMaxConsumption;
      float foodProd <- (rnd(1000) / 1000) * maxFoodProdRate;
      float food <- 0.0 update: food + foodProd; 
   }
}
```

Each cell of a grid will be an agent. Although a grid represent a particular species of agents with a specific topology, it is defined exactly like other species, with [attributes](Variables16.md), [actions](ActionGAMA16.md), [behaviors](Behaviors16.md) and [aspects](Aspect16.md).

# <font color='blue'>Experiments</font>

Experiment agents, which are able to take in charge the execution of simulations on the model, can also be defined in the model. Unlike other agents, they do not "belong" to the world. Two kinds of experiment are supported: gui (graphic user interface) and batch (exploration of models).

Example:

```
experiment my_experimentation type: gui {
   output {
      display stupid_display {
         grid stupid_cell;
         species bug aspect: basic;
      }
   }
} 
```

More details about experiments are given [here](experiment16.md).