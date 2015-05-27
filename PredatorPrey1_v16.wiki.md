
<br />
# <font color='blue'>Purpose</font>

Illustrate how to define a species of agents and parameters

# <font color='blue'>Formulation</font>
  * Definition of the **prey** species
  * Definition of a **nb\_prey\_init** parameter
  * Creation of **nb\_prey\_init** **prey** agents randomly located in the environment (size: 100x100)


# <font color='blue'>Model</font>

## Model structure
A GAMA model is composed of three sections:
  * **global** : this section defines the "world" agent, a special agent of a GAMA model. It represents all that is global to the model: dynamics, variables, actions. In addition, it allows to initialize the simulation (init block)
  * **entities** : this section defines the species of agents composing the model
  * **experiment** : this section define the input (parameters) and output (displays, files...) of a model.

More details about the different sections of a GAMA model can be found [here](Sections16.md).

## Entities
The entities section allows to define species of agents. A species represents a «prototype» of agents: it defines their common properties.

A species includes several sub-definitions:
  * the internal state of its agents (variables)
  * their behavior
  * how they are displayed (aspects)

Concerning the internal state, a [variable](Variables16.md) is defined as follows: type of the variable or const + name
  * For constants, a mandatory facet is **type** : int (integer), float (floating point number), string, bool (boolean, true or false), point (coordinates), list, pair, map, file, matrix, espèce d’agents, rgb (color), graph, path…
  * Optional facets: <- (initial value), update (value recomputed at each step of the simulation), function:{..} (value computed each time the variable is used), min, max

Note that all the species inherit from predefined built-in variables (see [here](BuiltInVariables16.md)):
  * A name (_name_)
  * A shape (_shape_)
  * A location (_location_) : the centroid of its shape.

Concerning the display of an agent, [aspects](Aspect16.md) have to be defined. An aspect represents a possible way to display the agents of a species : aspect aspect\_name {…}
In the block of an aspect, it is possible to draw :
  * A geometry :  for instance, the shape of the agent
  * An image : to draw icons
  * A text : to draw a text

In this first model, we define one species of agents: the **prey** agents. These agents will not have a particular behavior, they will just be displayed.
For each of these species, we define two new constant variables:
  * **size** of type float, with for initial value: 1.0
  * **color** of type _rgb_, with for initial value: "blue"

We define an aspect for this species. In this model, we want to display for each prey agent a circle of radius _size_ and color _color_. We then use the keyword **draw** with the facet **shape** that allows to draw a shape (circle, square, rectangle, triangle, line...).

```
entities {
   species prey {
      const size type: float <- 1.0 ;
      const color type: rgb <- rgb("blue");
      
      aspect base {
         draw circle(size) color: color ;
      }
   }
} 
```


## Global section
The global section represents the definition of the species of a specific agent (called world).
The world agent represents everything that is global to the model : dynamics, variables…
It allows to init simulations (init block): the world is always created and initialized first when a simulation is launched. The geometry (shape) of the world agent is by default a square with 100m for side size, but can be redefined if necessary (see the [Road traffic tutorial](GISTutorialRoadTraffic16.md)).

### Global variable
Definition of the a global variable of type _int_ concerning the number of _prey_ agents:
```
global {
   int nb_preys_init <- 200 min: 1 max: 1000 ;
}
```

### Model initialisation

The init section of the global block allows to initialize the model.
The statement _create_ allows to create agents of a specific species: **create** species\_name + :
  * number : number of agents to create (int, 1 by default)
  * from : GIS file to use to create the agents (string or file)
  * returns: list of created agents (list)

Definition of the init block in order to create _nb\_preys\_init_ _prey_ agents:
```
   init {
      create prey number: nb_preys_init ;
   }
```

## Experiment
An experiment block defines how a model can be simulated (executed). Several experiments can be defined for a model. They are defined using : **experiment** exp\_name type: gui/batch {`[input]` `[output]`}
  * gui : experiment with a graphical interface, which displays its input parameters and outputs.
  * batch : Allows to setup a series of simulations (w/o graphical interface).

In our model, we define a gui experiment called _prey\_predator_ :
```
experiment prey_predator type: gui {
}
```

### Input
Experiments can define (input) parameters. A parameter definition allows to make the value of a global variable definable by the user through the graphic interface.

A parameter is defined as follows:
**parameter** title var: global\_var category: cat;
  * **title** : string to display
  * **var** : reference to a global variable (defined in the global section)
  * **category** : string used to «store» the operators on the UI - optional

In the experiment, definition of a parameter from the the global variable _nb\_preys\_init_ :
```
experiment prey_predator type: gui {
   parameter "Initial number of preys: " var: nb_preys_init category: "Prey" ;
}
```

### Output
Output blocks are defined in an experiment and define how to visualize a simulation (with one or more display blocks that define separate windows). Each display can be refreshed independently by defining the facet **refresh\_every:** nb (int) (the display will be refreshed every nb steps of the simulation).

Each display can include different layers (like in a GIS) :
  * Agents lists : **agents** layer\_name value: agents\_list aspect: my\_aspect;
  * Agents species : **species**  my\_species aspect: my\_aspect
  * Images: **image** layer\_name file: image\_file;
  * Texts : **texte** layer\_name value: my\_text;
  * Charts : see later.

Note that it is possible to define a [opengl display](Gama3D16.md) (for 3D display) by using the facet **type: opengl**.

In our model, we define a display to draw the _prey_ agents.
```
 output {
      display main_display {
         species prey aspect: base ;
      }
   }
```

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
      const color type: rgb <- rgb("blue");
      
      aspect base {
         draw circle(size) color: color ;
      }
   }
} 

experiment prey_predator type: gui {
   parameter "Initial number of preys: " var: nb_preys_init category: "Prey" ;
   output {
      display main_display {
         species prey aspect: base ;
      }
   }
} 
```