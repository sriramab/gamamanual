# 1. Basic Model
This first step Illustrates how to write a model in GAMA. In particular, it describes how to structure a model and how to define species - that are the key components of GAMA models.
## Content


<br />

---


## Formulation
  * Definition of the **prey** species
  * Definition of a **nb\_prey\_init** parameter
  * Creation of **nb\_prey\_init** **prey** agents randomly located in the environment (size: 100x100)

<br />

---

## Model Definition

### model structure
A GAMA model is composed of three type of sections:
  * **global** : this section, that is unique, defines the "world" agent, a special agent of a GAMA model. It represents all that is global to the model: dynamics, variables, actions. In addition, it allows to initialize the simulation (init block).
  * **species** and **grid**: these sections define the species of agents composing the model. Grid are defined in the following model step "vegetation dynamic";
  * **experiment** : these sections define a context of execution of the simulations. In particular, it defines the input (parameters) and output (displays, files...) of a model.

More details about the different sections of a GAMA model can be found [here](G__OrganizationModel.md).


### Graphical modelling
First, you need to create a new project (File > New Gama Project). Then, you can create your first diagram ( Right click on your project > New > Other > Model Diagram).
For more details, you can refer to [Graphic model introduction](G__GamlEditor#Creating_a_first_model.md).

You should obtain a skeleton diagram similar to the following one.
<br />
<img src='https://gama-platform.googlecode.com/svn/wiki/images/Tutorials/Graphic_modelling1/01_Skeleton.png' />
<br />
### species
A [species](G__DefiningSpecies.md) represents a «prototype» of agents: it defines their common properties.

A species definition requires the definition of three different elements :
  * the internal state of its agents (attributes)
  * their behavior
  * how they are displayed (aspects)

#### Internal state
An [attribute](G__DefiningAttributes.md) is defined as follows: type of the attribute  and name. Numerous types of attributes are available: _int (integer), float (floating point number), string, bool (boolean, true or false), point (coordinates), list, pair, map, file, matrix, espèce d’agents, rgb (color), graph, path..._
  * Optional facets: <- (initial value), update (value recomputed at each step of the simulation), function:{..} (value computed each time the variable is used), min, max

In addition to the attributes the modeler explicitly defines, species "inherits" other attributes called "built-in" variables:
  * A name (_name_): the identifier of the species
  * A shape (_shape_): the default shape of the agents to be construct after the species. It can be _a point, a polygon, etc._
  * A location (_location_) : the centroid of its shape.

#### Behavior
In this first model, we define one species of agents: the **prey** agents. For the moment, these agents will not have a particular behavior, they will just exist and be displayed.

#### Display
An agent [aspects](G__DefiningAspects.md) have to be defined. An aspect is a way to display the agents of a species : aspect aspect\_name {…}
In the block of an aspect, it is possible to draw :
  * A geometry :  for instance, the shape of the agent (but it may be a different one, for instance a disk instead of a complex polygon)
  * An image : to draw icons
  * A text : to draw a text


#### Graphical modelling
To create any element in a GAMA diagram, you can use the palette (shown below). In the present case, we want to create a new species which is part of the 'world'. Thus, we use the tool "is composed of a species" then click on the "world" element and then outside of it and finally you name it.

<br />
<img src='https://gama-platform.googlecode.com/svn/wiki/images/Tutorials/Graphic_modelling1/02_Palette.png' />
<br />

To make our agent visible in the display, we need to edit the species, you do so by double clicking on the species element you just created. You will see a dialog similar to the following one.
<br />
<img src='https://gama-platform.googlecode.com/svn/wiki/images/Tutorials/Graphic_modelling1/05_Empty_Species.png' />
<br />

Instead of adding two variables (size and color) as in the [tutorial prey-predator](Tutorial__PredatorPreyTutorial_step1.md), we will use the built-in definition of the aspect. To do so, click on _has the aspect_ in the palette and add it to your _prey_ species. Then, double click on it and **add** a _layer_. In the opened dialog, make sure that the _Shape_ is a circle, _radius_ is 1.0 and the _color_ is blue as show in the image below.
<br />
<img src='https://gama-platform.googlecode.com/svn/wiki/images/Tutorials/Graphic_modelling1/06_Aspect_definition.png' />
<br />

### World element
In a GAMA model, we have a global agent, called the **World**, that includes all the other ones.
The world agent represents everything that is global to the model : dynamics, variables…
It allows to initialize simulations (init block): the world is always created and initialized first when a simulation is launched (before any other agents). The geometry (shape) of the world agent is by default a square with 100m for side size, but can be redefined if necessary (see the [Road traffic tutorial](Tutorial__RoadTrafficTutorial.md)).

#### global variable


In the current model, we will only have a certain numbers of preys thus we need to hold this number in a global or world's variable of type integer (_int_). To do so, edit the "world" species (double click on it) and add it a variable called _nb\_preys\_init_ of type _int_ and set its initial value to 200.


#### Model initialization

The init section of the global block allows to initialize the model: which is executing certain commands, here we will create _nb\_preys\_init_ number of prey agents. We use the statement _create_  to create agents of a specific species: **create** species\_name + :
  * number : number of agents to create (int, 1 by default)
  * from : GIS file to use to create the agents (optional, string or file)
  * returns: list of created agents (list)


Definition of the init block actually require to type a bit of code but it is pretty short and easy as you can see below:
```
      create prey number: nb_preys_init ;
```

<br />
<img src='https://gama-platform.googlecode.com/svn/wiki/images/Tutorials/Graphic_modelling1/03_world_definition.png' />
<br />

### experiment
An experiment defines how a model can be simulated (executed). Several experiments can be defined for a given model. As you have may have noticed, the graphical modelling editor already defined one by default, called  _my\_GUI\_xp,_ and attached to the _World_.

#### input
Experiments can define (input) parameters. A parameter definition allows to make the value of a global variable definable by the user through the graphic interface.

A parameter is defined as follows:
**parameter** title var: global\_var category: cat;
  * **title** : string to display
  * **var** : reference to a global variable (defined in the global section)
  * **category** : string used to «store» the operators on the UI - optional
  * **<-** : init value - optional
  * **min** : min value - optional
  * **max** : min value - optional

Note that the init, min and max values can be defined in the global variable definition.


To define a parameter, double click on the _my\_GUI\_xp_, add a parameter and fill in the fields as follows:

<br />
<img src='https://gama-platform.googlecode.com/svn/wiki/images/Tutorials/Graphic_modelling1/04_GUI_experiment.png' />
<br />
In the experiment, definition of a parameter from the the global variable _nb\_preys\_init_ :

#### output
Output blocks are defined in an experiment and define how to visualize a simulation (with one or more display blocks that define separate windows). Each display can be refreshed independently by defining the facet **refresh\_every:** nb (int) (the display will be refreshed every nb steps of the simulation).

Each display can include different layers (like in a GIS) :
  * Agents lists : **agents** layer\_name value: agents\_list aspect: my\_aspect;
  * Agents species : **species**  my\_species aspect: my\_aspect
  * Images: **image** layer\_name file: image\_file;
  * Texts : **texte** layer\_name value: my\_text;
  * Charts : see later.

Note that it is possible to define a [opengl display](G__3DSpecificInstructions.md) (for 3D display) by using the facet **type: opengl**.


The last part we need to do now is to add a display to visualise our _prey_ agents. Select "has the display" from the palette and add it to _my\_GUI\_xp_. Double click on it to edit, then add a layer. In the opened dialog (shown below), select _type_ to be species, _Species_ as prey and _aspect_ as default.

<br />
<img src='https://gama-platform.googlecode.com/svn/wiki/images/Tutorials/Graphic_modelling1/07_Display_Layer_definition.png' />
<br />

You can now start the simulation by clicking on the _Experiment my\_GUI\_xp_ on the top left corner of your graphical model.



---

## Complete Model

<br />
<img src='https://gama-platform.googlecode.com/svn/wiki/images/Tutorials/Graphic_modelling1/08_Step1_complete_model.png' />
<br />