# 1. Creation of a first basic disease spreading model
This first step illustrates how to create simple agent and make them move in their environment.


![https://github.com/gama-platform/gama/wiki/images/Tutorials/Luneray's flu/luneray1.tiff](https://github.com/gama-platform/gama/wiki/images/Tutorials/Luneray's flu/luneray1.tiff)




## Formulation
  * Set the time duration of a time step to 1 minutes
  * Define the people species with a moving skill
  * Define the move reflex that allow the people agent to move randomly and the infect reflex that allows them to infect other people agents.
  * Define the aspect of the people species
  * Add the people species to a display



## Model Definition

### Project and model
The first step of this tutorial consists in launching GAMA and choosing a workspace, then to define a new project or to import the existing one. For people that do not want to re-write all the models but just to follow the model construction, they can just download the model project here and the follow this [procedure](G__ImportingModels) to import it into GAMA. For the other, the project and model creation procedures are detailed [here](G__GamlEditor). 

Note that the concepts of workspace and projects are explained [here](G__Workspace).


### model structure
A GAMA model is composed of three type of sections:
  * **global** : this section, that is unique, defines the "world" agent, a special agent of a GAMA model. It represents all that is global to the model: dynamics, variables, actions. In addition, it allows to initialize the simulation (init block).
  * **species** and **grid**: these sections define the species of agents composing the model. Grid are defined in the following model step "vegetation dynamic";
  * **experiment** : these sections define a context of execution of the simulations. In particular, it defines the input (parameters) and output (displays, files...) of a model.

More details about the different sections of a GAMA model can be found [here](G__OrganizationModel).

### species
A [species](G__DefiningSpecies) represents a «prototype» of agents: it defines their common properties.

Three different elements can be defined in a species:
  * the internal state of its agents (attributes)
  * their behavior
  * how they are displayed (aspects)

In our model, we define a people species:
```
species people {
		 
}
```

In addition, we want add a new capability to our agent: the possibility to move randomly. for that, we add a specific skill to our people agents. A [skill](G__Skills) is a built-in module that provide the modeler a self-contain and relevant set of actions and variables. The [moving](__BuiltInSkills#moving) provides the agents with several attributes and actions related to movement. 

```
   species people skills: [moving]{
       ...
   }
```


#### Internal state
An [attribute](G__DefiningAttributes) is defined as follows: type of the attribute  and name. Numerous types of attributes are available: _int (integer), float (floating point number), string, bool (boolean, true or false), point (coordinates), list, pair, map, file, matrix, espèce d’agents, rgb (color), graph, path..._
  * Optional facets: <- (initial value), update (value recomputed at each step of the simulation), function:{..} (value computed each time the variable is used), min, max

In addition to the attributes the modeler explicitly defines, species "inherits" other attributes called "built-in" variables:
  * A name (_name_): the identifier of the species
  * A shape (_shape_): the default shape of the agents to be construct after the species. It can be _a point, a polygon, etc._
  * A location (_location_) : the centroid of its shape.

In our model, we define 2 new attribute to our people agents: 
  * **speed** of type float, with for initial value: a random value between 2 and 5 km/h
  * **is_infected** of type bool, with for initial value: false

```
species people skills:[moving]{		
	float speed <- (2 + rnd(3)) #km/#h;
	bool is_infected <- false;
}
```
Note we use the [rnd](G__Operators#rnd) operator to define a random value between 2 and 5 for the speed. In addition, we precise a unit for the speed value by using the # symbol. For more details about units, see [here](G__UnitsAndConstants).

#### Behavior
GAMA proposes several ways to define the behavior of a species: dynamic variables (update facet), reflexes....

A [reflex](G__DefiningBehaviors#reflex) is a block of statements (that can be defined in global or any species) that will be automatically executed at each simulation step if its condition is true, it is defined as follows:
```
   reflex reflex_name when: condition {…}
```

The **when** facet is optional: when it is omitted, the reflex is activated at each time step. Note that if several reflexes are defined for a species, the reflexes will be activated following their definition order.

We define a first reflex called **move** that is activated at each simulation step (no condition) and that makes the people move randomly using the wander action from the [moving](G__BuiltInSkills#moving) skill.
```
species people skills:[moving]{		
	//variable definition
	reflex move{
		do wander;
	}
}
```

We define a second reflex called **infect** that is activated only when the agent is infected (is_infected = true) and that ask all the people at a distance of 10m to test a probability to be infected.
```
species people skills:[moving]{		
	//variable definition and move reflex
	
	reflex infect when: is_infected{
		ask people at_distance 10 #m {
			if flip(0.05) {
				is_infected <- true;
			}
		}
	}
}
```
The [ask](G__Statements#ask) allows an agent to ask another agents to do something (i.e. to execute a sequence of statements). The [at_distance](G__Operators#at_distance) operator allows to get the list of agents (here of people agents) that are located at a distance lower or equal to the given distance (here 10m). The [flip](G__Operators#flip) operator allows to test a probability.

#### Display
An agent [aspects](G__DefiningAspects) have to be defined. An aspect is a way to display the agents of a species : aspect aspect\_name {…}
In the block of an aspect, it is possible to draw :
  * A geometry :  for instance, the shape of the agent (but it may be a different one, for instance a disk instead of a complex polygon)
  * An image : to draw icons
  * A text : to draw a text

In our model, we define an aspect for the people agent called **circle** that draw the agents as a circle of 10m radius with a color that depends on their **is_infected** attribute. If the people agent is infected, it will be draw in red, in green otherwise.

```
species people {
	...//variable and reflex definition

	aspect circle {
			draw circle(10) color:is_infected ? #red : #green;
		}
	} 
}
```
The **?** structure allows to return a different value (here red or green) according to a condition (here is_infected = true).

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