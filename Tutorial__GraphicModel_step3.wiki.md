# 3. Prey Agent Behavior
This third step Illustrates how to define the behaviors of prey agents and the concept of spatial topology.

<br />

---


## Formulation
  * Random movement of the prey agents to a distance of 2 cells (Von Neumann neighborhood)
  * At each step, the prey agents loss energy
  * At each step, the prey agents eat food if there is food on the cell on which they are localized (with a max of max\_transfer) and gain energy
  * If a prey agent has no more energy, it dies

<br />

---

## Model Definition

### parameters
To define a behavior for the prey agents we add them three new parameters:
  * The max energy of the prey agents (init equals to 1.0)
  * The maximum energy that can a prey agent consume from vegetation per tick (init equals to 0.1)
  * The energy used by a prey agent at each time step (init equals to 0.05)

Similarly to the definition of _nb\_preys\_init_ (cf. [step1](Tutorial__GraphicModel_step1.md)), you will have to add these parameters as global variables to the _World_. Double click on the _World_ item to edit it, click on _add variable_ and add the following definitions:
<br />
<img src='https://gama-platform.googlecode.com/svn/wiki/images/Tutorials/Graphic_modelling1/13_Prey_global_variables.png' />
<br />


Yet we may allow the user to change it from an experiment to another through the user interface. To do so we refer to these global parameters in _my\_GUI\_xp_ as follows :
<br />
<img src='https://gama-platform.googlecode.com/svn/wiki/images/Tutorials/Graphic_modelling1/14_Prey_global_parameters.png' />
<br />



### vegetation\_cell grid
We add a new variable for the vegetation\_cell grid called **neighbours**, that contains for each vegetation cell the list of the neighbor vegetation cells (distance of 2 - Von Neumann neighborhood). We will use these list of vegetation\_cell neighbours for the movement of the prey.
<br />
<img src='https://gama-platform.googlecode.com/svn/wiki/images/Tutorials/Graphic_modelling1/15_vegetation_neighbours.png' />
<br />


Note that the result of the operator **neighbours\_at dist** depends on the type of topology of the agent applying this operator:
  * For a grid topology (grid species), the operator returns the neighbor cells (with a Von Neumann or Moore neighborhood).
  * For a continuous topology, the operator returns the list of agents of which the shape is located at a distance equals or inferior _dist_ meters to the agent shape.

Also note the use of the [self](G__PseudoVariables#self.md) pseudo variable which is a reference to the agent currently executing the statement

## Prey agents

We copy the values of the three global parameters into the prey species in order for it to be available for each agent and possibly modified locally. To do so, you simply create 3 new variables in the prey species. We also add a variable representing the energy used by each prey at each timestep as a randomly computed initially number (within ]0;max\_energy]).
<br />
<img src='https://gama-platform.googlecode.com/svn/wiki/images/Tutorials/Graphic_modelling1/16_prey_energy_variables.png' />
<br />



In order to define the movement behaviour of a prey we will add a **reflex**. A reflex is a block of statements (that can be defined in global or any species) that will be automatically executed at each simulation step if its condition is true, Select the _has the reflex_ from the palette and add it to the prey species. Then double click on it to edit it, name it **basic\_move** and put the following code into the _Gaml code_ text pane.
```
       myCell <- one_of (myCell.neighbours) ;
       location <- myCell.location ;
```


The **when** facet is optional: when it is omitted, the reflex is activated at each time step. Note that if several reflexes are defined for a species. This first reflex allows the prey agents to choose (randomly) a new vegetation\_cell in the neighborhood of my\_cell and to move to this cell.
<br />
<img src='https://gama-platform.googlecode.com/svn/wiki/images/Tutorials/Graphic_modelling1/17_Prey_basic_move.png' />
<br />




Similarly, We define a second reflex called **eat** that will only be activated when there is food in my\_cell and that will allows the prey agents to eat food and gain energy. In order to store the energy gain by the eating (that is equals to the minimum between the **max\_transfer** value and the quantity of food available in **myCell**), we define a local variable called **energy\_transfer**.  A local variable is a variable that will only exist within this block: once it has been executed, the variable is forgotten. As previously, create a new reflex named **eat**. This time it will have a _when_ condition : `myCell.food > 0`and the following Gaml code:

```
      float energy_transfer <- min([max_transfer, myCell.food]) ;
      myCell.food <- myCell.food - energy_transfer ;
      energy <- energy + energy_transfer ;
```

<br />
<img src='https://gama-platform.googlecode.com/svn/wiki/images/Tutorials/Graphic_modelling1/18_Prey_eat.png' />
<br />




We define a third reflex for the prey agent: when the agent has no more energy, it dies (application of the built-in **die** action). In this case the condition is `energy <= 0`and the gaml code is `do die ;`.

<br />
<img src='https://gama-platform.googlecode.com/svn/wiki/images/Tutorials/Graphic_modelling1/19_Prey_die.png' />
<br />


Note that an action is a capability available to the agents of a species (what they can do). It is a block of statements that can be used and reused whenever needed. Some actions, called primitives, are directly coded in Java: for instance, the **die** action defined for all the agents.
  * An action can accept arguments. For instance, write takes an argument called message.
  * An action can return a result.

There are two ways to call an action: using a statement or as part of an expression
  * for actions that do not return a result:
```
do action_name arg1: v1 arg2: v2;
```

  * for actions that return a result:
```
my_var <- self action_name (arg1:v1, arg2:v2);
```

<br />

---

## Complete Model
<br />
<img src='https://gama-platform.googlecode.com/svn/wiki/images/Tutorials/Graphic_modelling1/20_Step3_complete_model.png' />
<br />