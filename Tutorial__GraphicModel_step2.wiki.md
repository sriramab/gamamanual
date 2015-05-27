# 2. Vegetation Dynamic
This second steps present the idea of environment or topological space. Defining a "vegetation" environment allows to define the movement of the preys through dynamic variables (use of the _update_ facet). We will also discover more about displays.



<br />

---


## Formulation
  * Definition of a grid (for the vegetation)
  * Definition of a dynamic for each cell (food production)
  * Display of the cell color according to the quantity of food
  * Localization of the prey agents on the cells (at its center)

<br />

---

## Model Definition

### grid

In GAMA, grids are specific agent species with a particular topology. First, a grid allow yet constrains the movement of other (moving) agents but they can also have variables and behaviors.

To add a grid to your model, use _is composed of grid_ from the palette and link it to the _world_. Then double click to edit this new grid.  We will call it **vegetation\_cell** and modify its properties as follows: neighbourhood "4 - Von Neumann", 50 rows and 50 columns.


In order for each grid agents (or cell of the grid) to represent the vegetation, we provide them with four variables. To do so, click on _Add variable_ in the _Variables_ pane as follows:

  * _maxFood_ : maximum food that a cell can contain. type: _float_ ; init value: 1.0
  * _foodProd_ : food produced at each simulation step. type: _float_ ; init value: random number between 0 and 0.01
  * _food_ : current quantity of food. type: _float_ ; init value: random number between 0 and 1.0; at each simulation step : food <- food + foodProd
  * _color_ : color of the cell. type: _rgb_ ; init value: color computed according to the food value: more the food value is close to 1.0, greener the color is, more the food value is close to 0,  whiter the color is; update : computation of the new color depending on the current level of food (at each simulation step).


To give these cells a dynamics, we need to provide them with **update\*s. The _food_ update, representing the food production, is _" (rnd(1000) / 1000) update: food + foodProd"_ and we limit its maximum value with the global _maxFood_ variable defined in the World agent (same goes for _foodProd_). We will also update the _color_ variable to reflect the change of food level, to do so, we simply copy/paste the initial expression in the update field : **rgb(int(255** (1 - food)), 255, int(255 _(1 - food)))_.**


Defining the 3 rgb components of a color is not the only way to define a color in GAML:
  * the simplest way consists in using the symbol _#_ + the color name (for a limited set of  [colors](G__Index#Constants_and_colors.md)):
```
   #blue
   #red
```
  * Another way consists in defining the 3 rgb integer values: rgb(red, green, blue) with red, green and blue between 0 and 255 (as we used in the current model.
```
   rgb(0,0,0) : black ; rgb(255,255,255) : white
   rgb(255,0,0) : red ;  rgb(0,255,0) : green ;  rgb(0,0,255) : blue
```


You should obtain the following definition of the **vegetation\_cell** :
<br />
<img src='https://gama-platform.googlecode.com/svn/wiki/images/Tutorials/Graphic_modelling1/09_VegetationCell.png' />
<br />

### prey agents
In order to relate our prey agents to the vegetation cell grid, we add them with one new variable : **my\_cell** of type vegetation\_cell and for init value one of the vegetation\_cell (chosen randomly).  Double click the _prey_ species and add it a variable called _myCell_ of type _vegetation\_cell_ and with _initial value_  equals to _one\_of (vegetation\_cell)_.
Using the name of a species as a keyword returns the list of all agent of this species (_vegetation\_cell_ here) while **one\_of** selects randomly one element from a list.


We linked each prey agent to a vegetation\_cell but we need to locate them onto the cell initially. To do so, we edit the init block in the prey species with _"location <- myCell.location;"_ . It sets the prey location as equals to the location of the vegetation cell (i.e. its centroid **location**),  the **<-** statement that allows to modify the value of a variable.

<br />
<img src='https://gama-platform.googlecode.com/svn/wiki/images/Tutorials/Graphic_modelling1/10_Prey_init_location.png' />
<br />

### display
Finally, we need to update our display to show the vegetation. Logically, we need to edit the _my\_display_ element and add it a new layer. This layer is of type _grid_ and the _grid_ being called _vegetation\_cell_. To make it clearer, we also check the _Show Lines_ option. You should obtain a display similar to the following one:

<br />
<img src='https://gama-platform.googlecode.com/svn/wiki/images/Tutorials/Graphic_modelling1/11_Display_grid.png' />
<br />
Note that the layers in a display work like layers in a GIS; the drawing order will be respected. In our model, the prey agents will be drawn above the vegetation\_cell grid thus they need to be declared afterward.
<br />

---

## Complete Model

<br />
<img src='https://gama-platform.googlecode.com/svn/wiki/images/Tutorials/Graphic_modelling1/12_Step2_complete_model.png' />