# Grid Species

A grid is a particular species of agents. Indeed, a grid is a set of agents that share a grid topology (until now, we only saw species with continuous topologies). As other agents, a grid species can have attributes, attributes, behaviors, aspects
However, contrary to regular species, grid agents are created automatically at the beginning of the simulation. It is thus not necessary to use the create statement to create them.
Moreover, in addition to classic built-in variables, grid a provided with a set of additional built-in variables.

## Index

* [Declaration](#declaration)
* [Built-in attributes](#built-in-attributes)
* [Access to cells](#access-to-cells)
* [Display grid](#display-grid)
* [Grid with matrix](#grid-with-matrix)
* [Example](#example)

## Declaration

Instead of using the `species` keyword, use the keyword `grid` to declare a grid species. The grid species has exactly the same facets of the regular species, plus some others.
To declare a grid, you have to specify the number of columns and rows first. You can do it two different ways:

Using the two facets `weight:` and `height:` to fix the number of cells (the size of each cells will be determined thanks to the environment dimension).

```
grid my_grid width:8 height:10 {
// my_grid has 8 columns and 10 rows
}
```

Using the two facets `cell_weight:` and `cell_height:` to fix the size of each cells (the number cells will be determined thanks to the environment dimension).

```
grid my_grid cell_width:3 cell_height:2 {
// my_grid has cells with dimension 3m width by 2m height
}
```

By default, a grid is composed by 100 rows and 100 columns.

Another facet exists for grid only, very useful. It is the `neighbors` facet, used to determine how many neighbors has each cell. You can choose among 3 values: 4 (Von Neumann), 6 (hexagon) or 8 (Moore).

(TODO_IMAGE)

A grid can also be provided with specific facets that allows to optimized the computation time and the memory space, such as `use_regular_agents`, `use_indivitual_shapes` and `use_neighbours_cache`. Please refer to the GAML Reference for more explanation about those particular facets.

Built-in attributes

Cf wiki

Access to a grid

Cf wiki
+ grid_at

Display a grid

Cf wiki

Grid with matrix

TODO

Example

To practice a bit those notions, we will build a quick model. A "regular" species will move randomly on the environment. A grid is displayed, and its cells becomes red when an instance of the regular species is waking inside this cell, and yellow when the regular agent is in the surrounding of this cell. If no regular agent is on the surrounding, the cell turns green.

 

Here is an example of implementation:

model my_grid_model

global{
	float max_range <- 5.0;
	int number_of_agents <- 5;
	init {
		create my_species number:number_of_agents;
	}
	reflex update {
		ask my_species {
			do wander amplitude:180;	
			ask my_grid at_distance(max_range)
			{
				if(self overlaps myself)
				{
					self.color_value <- 2;
				}
				else if (self.color_value != 2)
				{
					self.color_value <- 1;
				}
			}
		}
		ask my_grid {
			do update_color;
		}	
	}
}

species my_species skills:[moving] {
	float speed <- 2.0;
	aspect default {
		draw circle(1) color:#blue;
	}
}

grid my_grid width:30 height:30 {
	int color_value <- 0;
	action update_color {
		if (color_value = 0) {
			color <- #green;
		}
		else if (color_value = 1) {
			color <- #yellow;
		}
		else if (color_value = 2) {
			color <- #red;
		}
		color_value <- 0;
	}
}

experiment MyExperiment type: gui {
    output {
        display MyDisplay type: java2D {
            grid my_grid lines:#black;
            species my_species aspect:default; 
        }
    }
}