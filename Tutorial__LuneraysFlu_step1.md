# 1. Creation of a first basic disease spreading model
This first step illustrates how to create simple agent and make them move in their environment.


![https://github.com/gama-platform/gama/wiki/images/Tutorials/Luneray's flu/luneray1.tiff](https://github.com/gama-platform/gama/wiki/images/Tutorials/Luneray's flu/luneray1.tiff)




## Formulation
  * Set the time duration of a time step to 1 minutes
  * Define the people species with a moving skill
  * Define the move and the infect behaviors of the people species
  * Define the aspect of the people species
  * Add the people species to a display



## Model Definition
### model structure
A GAMA model is composed of three type of sections:
  * **global** : this section, that is unique, defines the "world" agent, a special agent of a GAMA model. It represents all that is global to the model: dynamics, variables, actions. In addition, it allows to initialize the simulation (init block).
  * **species** and **grid**: these sections define the species of agents composing the model. Grid are defined in the following model step "vegetation dynamic";
  * **experiment** : these sections define a context of execution of the simulations. In particular, it defines the input (parameters) and output (displays, files...) of a model.

More details about the different sections of a GAMA model can be found [here](G__OrganizationModel).

### species
A [species](G__DefiningSpecies) represents a «prototype» of agents: it defines their common properties.

A species definition requires the definition of three different elements :
  * the internal state of its agents (attributes)
  * their behavior
  * how they are displayed (aspects)

#### Internal state
An [attribute](G__DefiningAttributes) is defined as follows: type of the attribute  and name. Numerous types of attributes are available: _int (integer), float (floating point number), string, bool (boolean, true or false), point (coordinates), list, pair, map, file, matrix, espèce d’agents, rgb (color), graph, path..._
  * Optional facets: <- (initial value), update (value recomputed at each step of the simulation), function:{..} (value computed each time the variable is used), min, max

In addition to the attributes the modeler explicitly defines, species "inherits" other attributes called "built-in" variables:
  * A name (_name_): the identifier of the species
  * A shape (_shape_): the default shape of the agents to be construct after the species. It can be _a point, a polygon, etc._
  * A location (_location_) : the centroid of its shape.

#### Behavior
In this first model, we define one species of agents: the **prey** agents. For the moment, these agents will not have a particular behavior, they will just exist and be displayed.

#### Display
An agent [aspects](G__DefiningAspects) have to be defined. An aspect is a way to display the agents of a species : aspect aspect\_name {…}
In the block of an aspect, it is possible to draw :
  * A geometry :  for instance, the shape of the agent (but it may be a different one, for instance a disk instead of a complex polygon)
  * An image : to draw icons
  * A text : to draw a text

In order to display our prey agents we define two attributes:
  * **size** of type float, with for initial value: 1.0
  * **color** of type _rgb_, with for initial value: "blue". It is possible to get a color value by using the symbol _#_ + color name: e.g. #blue, #red, #white, #yellow, #magenta, #pink...

### species






## Complete Model

```
model SI_city1

global{ 
	int nb_people <- 2147;
	int nb_infected_init <- 5;
	float step <- 1 #mn;
	geometry shape<-square(1500 #m);
	
	init{
		create people number:nb_people;
		ask nb_infected_init among people {
			is_infected <- true;
		}
	}
	
}

species people skills:[moving]{		
	float speed <- (2 + rnd(3)) #km/#h;
	bool is_infected <- false;
	reflex move{
		do wander;
	}
	reflex infect when: is_infected{
		ask people at_distance 10 #m {
			if flip(0.05) {
				is_infected <- true;
			}
		}
	}
	aspect circle{
		draw circle(10) color:is_infected ? #red : #green;
	}
}

experiment main_experiment type:gui{
	parameter "Nb people infected at init" var: nb_infected_init min: 1 max: 2147;
	output {
		display map type: opengl{
			species people aspect:circle;			
		}
	}
}
```