# 1. Creation of a first basic disease spreading model
This first step illustrates how to create simple agents and make them move in their environment.


![https://github.com/gama-platform/gama/wiki/images/Tutorials/Luneray's flu/luneray2.tiff](https://github.com/gama-platform/gama/wiki/images/Tutorials/Luneray's flu/luneray2.tiff)




## Formulation
  * Add three new global dynamic variables to follow the evolution of the number of infected people agents, of not infected people agents and of the rate of infected people.
  * Define an ending condition for the simulation
  * Define a monitor to follow the rate of infected people agents
  * Define a chart to follow the rate of infected people agents



## Model Definition


### global section

#### global variables

GAMA offers the possibility to define dynamic variable that will be recomputed at each simulation step by using the _update_ facet when defining a variable. When an agent is activated, first, it recomputes each of its variables with a update facet (in their definition order), then it activates each of its reflexes (in their definition order).

To better follow the evolution of sick people, we add three new global variables to the model:
  * nb_people_infected of type _int_ with _nb\_infected\_init_ as init value and updated at each simulation step by the number of infected people
  * nb_people_not_infected of type _int_ with _(nb\_people - nb\_infected\_init)_ as init value and updated at each simulation step by the number of not infected people
  * infected_rate of type _float_ updated at each simulation step by the number of infected people divided by the number of people.

```
global{
	//... other attributes
	int nb_people_infected <- nb_infected_init update: people count (each.is_infected);
	int nb_people_not_infected <- nb_people - nb_infected_init update: nb_people - nb_people_infected;
	float infected_rate update: nb_people_infected/nb_people;
	//... init
}
```

We used the [count](G__Operators#count) operator that allows to count the number of elements of a list for which the left condition is true. The keyword _each_ represents each element of the list.

#### ending condition

The simplest way to add an ending condition to a model is to add a global reflex that is activated at the end of the simulation that will pause the simulation (use of the _pause_ global action).

In our model, we add a new reflex called _end\_simulation_ that will be activated when the infected rate is 1.0 (i.e. all the people agents are infected) and that will apply the _pause_ action. 
```
global {
	//.. variable and init definition
	
	reflex end_simulation when: infected_rate = 1.0 {
		do pause;
	}
} 
```
### experiment

#### input
Experiments can define (input) parameters. A parameter definition allows to make the value of a global variable definable by the user through the graphic interface.

A [parameter](__DefiningParameters) is defined as follows:
**parameter** title var: global\_var category: cat;
  * **title** : string to display
  * **var** : reference to a global variable (defined in the global section)
  * **category** : string used to «store» the operators on the UI - optional
  * **<-** : init value - optional
  * **min** : min value - optional
  * **max** : min value - optional

Note that the init, min and max values can be defined in the global variable definition.

#### output


## Complete Model

```
model SI_city2

global{ 
	int nb_people <- 2147;
	int nb_infected_init <- 5;
	float step <- 1 #mn;
	geometry shape<-square(1500 #m);
	int nb_people_infected <- nb_infected_init update: people count (each.is_infected);
	int nb_people_not_infected <- nb_people - nb_infected_init update: nb_people - nb_people_infected;
	float infected_rate update: nb_people_infected/nb_people;
	
	
	init{
		create people number:nb_people;
		ask nb_infected_init among people {
			is_infected <- true;
		}
	}
	
	reflex end_simulation when: infected_rate = 1.0 {
		do pause;
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
		monitor "Infected people rate" value: infected_rate;
		
		display map type: opengl{
			species people aspect:circle;			
		}
		
		display chart refresh_every: 10 {
			chart "Disease spreading" type: series {
				data "susceptible" value: nb_people_not_infected color: #green;
				data "infected" value: nb_people_infected color: #red;
			}
		}
	}
}
```