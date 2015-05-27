
<br />
# <font color='blue'>Purpose</font>

Illustrate how to define a grid and use it to constraint the movement of agents

# <font color='blue'>Formulation</font>
  * Definition of a grid (for the vegetation)
  * Definition of a dynamic for each cell (food production)
  * Display of the cell color according to the quantity of food
  * Localization of the prey agents on the cells (at its center)

# <font color='blue'>Model</font>

## Grid

In GAMA, grids are specific agent species with a particular topology. They can have variables and behaviors.
Grids have to be defined in the entities section.

A grid is defined as follows:
```
entities{
   ...
   grid grid_name width: nb_cols height: nb_lines neighbors: 4/6/8 {
      ...
   }
} 
```

With:
  * width : number of cells along x-axis
  * height : number of cells along y-axis
  * neighbours : neighborhood type (4 - Von Neumann, 6 - hexagon or 8 - Moore)

In our model, we define a grid species, called **vegetation\_cell** composed of 50x50 cells and with a Von Neumann neighborhood.
These agents have four variables:
  * _maxFood_ : maximum food that a cell can contain -> type: _float_ ; init value: 1.0
  * _foodProd_ : food produced at each simulation step -> type: _float_ ; init value: random number between 0 and 0.01
  * _food_ : current quantity of food -> type: _float_ ; init value: random number between 0 and 1.0; at each simulation step : food <- food + foodProd
  * _color_ : color of the cell -> type: _rgb_ ; init value: color computed according the food value: more the food value is close to 1.0, more the color is green, more the food value is close to 0, more the color is white; at each simulation step : computation of the new color.
```
entities{
   ...
   grid vegetation_cell width: 50 height: 50 neighbours: 4 {
      float maxFood <- 1.0 ;
      float foodProd <- (rnd(1000) / 1000) * 0.01 ;
      float food <- (rnd(1000) / 1000) update: food + foodProd max: maxFood;
      rgb color <- rgb(int(255 * (1 - food)), 255, int(255 * (1 - food))) update: rgb(int(255 * (1 - food)), 255, int(255 * (1 - food))) ;
   }
}
```

Note that there are several ways to define colors in GAML:
  * the simplest way consists in casting a string into a rgb value (only for some predefined colors):
```
   rgb("blue")
   rgb("red")
```
  * Another way consists in defining the 3 rgb integer values: rgb(red, green, blue) with red, green and blue between 0 and 255.
```
   rgb(0,0,0) : black ; rgb(255,255,255) : white
   rgb(255,0,0) : red ;  rgb(0,255,0) : green ;  rgb(0,0,255) : blue
```


## Prey agents
We add one new variables for the prey agents: **my\_cell** of type vegetation\_cell and for init value one of the vegetation\_cell (chosen randomly).

```
   species prey {
      ...
      vegetation_cell myCell <- one_of (vegetation_cell) ;
   } 
```

Note that it is possible to obtain the list of all agents of a given species by using the name of the species.

In order to locate the agent at the centroid of its vegetation cell (**location**), we use in the init block the **<-** statement that allows to modify the value of a variable :
```
   init {
         location <- myCell.location;
      }
```

## Display
We add the grid species in the display in order to display it. We use for that the statement **grid** with the optional facet **lines** to draw the border of the cells.
```
   output {
      display main_display {
         grid vegetation_cell lines: rgb("black") ;
         species prey aspect: base ;
      }
   }
```

Note that the layers in a display work like layers in a GIS; the drawing order will be respected. In our model, the prey agents will be drawn above the vegetation\_cell grid.

# <font color='blue'>Complete model</font>

```
model prey_predator

global {
   int nb_preys_init <- 200 min: 1 max: 1000 ;
   init {
      create prey number: nb_preys_init ;
   }
}
entities {
   species prey {
      const size type: float <- 1.0 ;
      const color type: rgb <- rgb("blue") ;
      vegetation_cell myCell <- one_of (vegetation_cell) ;
      
      init {
         location <- myCell.location;
      }
      
      aspect base {
         draw circle(size) color: color ;
      }
   }
   grid vegetation_cell width: 50 height: 50 neighbours: 4 {
      float maxFood <- 1.0 ;
      float foodProd <- (rnd(1000) / 1000) * 0.01 ;
      float food <- (rnd(1000) / 1000) update: food + foodProd max: maxFood;
      rgb color <- rgb(255 * (1 - food), 255, 255 * (1 - food)) update: rgb(255 * (1 - food), 255, 255 * (1 - food)) ;
   }
}
 
experiment prey_predator type: gui {
   parameter "Initial number of preys: " var: nb_preys_init category: "Prey" ;
   output {
      display main_display {
         grid vegetation_cell lines: rgb("black") ;
         species prey aspect: base ;
      }
   }
}
```