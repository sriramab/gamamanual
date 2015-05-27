
<br />
# <font color='blue'>Purpose</font>

Illustrate how to define agent behaviors and the concept of topology.

# <font color='blue'>Formulation</font>
  * Random moving of the prey agents to a distance of 2 cells (Von Neumann neighbors)
  * At each step, the prey agents loss energy
  * At each step, the prey agents eat food if there is food on the cell on which they are localized (with a max of max\_transfer) and gain energy
  * If a prey agent has no more energy, it dies


# <font color='blue'>Model</font>

## Parameters
We add of three new parameters:
  * The max energy of the prey agents
  * The maximum energy that can gain a prey agent while eating for a time step
  * The energy consumed by a prey agent at each time step

In the global section, definition of the three global variables:

```
   float prey_max_energy <- 1.0;
   float prey_max_transfer <- 0.1;
   float prey_energy_consum <- 0.05;
   
```

In the experiment, definition of the three corresponding parameters:
```
   parameter "Prey max energy: " var: prey_max_energy category: "Prey" ;
   parameter "Prey max transfer: " var: prey_max_transfer  category: "Prey" ;
   parameter "Prey energy consumption: " var: prey_energy_consum  category: "Prey" ;
```

## vegetation\_cell grid
We add a new variable for the vegetation\_cell grid called **neighbours**, that contains for each vegetation\_cell the list of the neighbor vegetation cells (distance of 2 - Von Neumann neighborhood).

```
  grid vegetation_cell width: 50 height: 50 neighbours: 4 {
      ...
      list<vegetation_cell> neighbours <- self neighbours_at 2;
   }
```

Note that the result of the operator **neighbours\_at dist** depends on the type of topology of the agent applying this operator:
  * For a grid topology (grid species), the operator returns the neighbor cells (with a Von Neumann or Moore neighborhood).
  * For a continuous topology, the operator returns the list of agents of which the shape is located at a distance equals or inferior _dist_ to the agent shape.

## Prey agents

```
      const max_energy type: float <- prey_max_energy ;
      const max_transfer type: float <- prey_max_transfer ;
      const energy_consum type: float <- prey_energy_consum ;
```

```
      float energy <- (rnd(1000) / 1000) * max_energy  update: energy - energy_consum max: max_energy ;
```



A reflex is a block of statements (that can be defined in global or any species) that will be automatically executed at each simulation step if its condition is true. A reflex is defined as follows:
```
   reflex reflex_name when: condition {…}
```

The **when** facet is optional: when it is omitted, the reflex is activated at each time step.

We define a first reflex called **basic\_move** that allows the prey agents to choose a new vegetation\_cell in the neighborhood of my\_cell and to move to this cell.
```
      reflex basic_move { 
         myCell <- one_of (myCell.neighbours) ;
         location <- myCell.location ;
      }
```

We define a second reflex called **eat** that will only be activated when there is food in my\_cell and that will allows the prey agents to eat food and gain energy. In order to store the energy gain by the eating (that is equals to the minimum between the **max\_transfer** value and the quantity of food in **myCell**), we define a local variable called **energy\_transfer**.  A local variable is a variable that will only exist within this block: once it has been executed, the variable is forgotten. To define it, we have to use the following statement:
```
var_type var_name <- value; 
```

Thus, the reflex **eat** is defined by:
```
      reflex eat when: myCell.food > 0 { 
         float energy_transfer <- min([max_transfer, myCell.food]) ;
         myCell.food <- myCell.food - energy_transfer ;
         energy <- energy + energy_transfer ;
      }
```

We define a third reflex for the prey agent: when the agent has no more energy, it dies (application of the **die** action):
```
      reflex die when: energy <= 0 {
         do die ;
      }
```

Note that an action is a capability available to the agents of a species (what they can do). It is a block of statements that can be used and reused whenever needed. Some actions, called primitives, are directly coded in Java : for instance, the **die** action defined for all the agents.
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


# <font color='blue'>Complete model</font>

```
model prey_predator

global {
   int nb_preys_init <- 200 min: 1 max: 1000 ;
   float prey_max_energy <- 1.0;
   float prey_max_transfer <- 0.1;
   float prey_energy_consum <- 0.05;
   init {
      create prey number: nb_preys_init ;
   }
}
entities {
   species prey {
      const size type: float <- 1.0 ;
      const color type: rgb <- rgb("blue") ;
      const max_energy type: float <- prey_max_energy ;
      const max_transfer type: float <- prey_max_transfer ;
      const energy_consum type: float <- prey_energy_consum;
      vegetation_cell myCell <- one_of (vegetation_cell) ;
      float energy <- (rnd(1000) / 1000) * max_energy  update: energy - energy_consum max: max_energy ;

      init {
         location <- myCell.location;
      }
      
      reflex basic_move { 
         myCell <- one_of (myCell.neighbours) ;
         location <- myCell.location ;
      }
      reflex eat when: myCell.food > 0 { 
         float energy_transfer <- min([max_transfer, myCell.food]) ;
         myCell.food <- myCell.food - energy_transfer ;
         energy <- energy + energy_transfer ;
      }
      reflex die when: energy <= 0 {
         do die ;
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
      list<vegetation_cell> neighbours <- self neighbours_at 2;
   }
}
 
experiment prey_predator type: gui {
   parameter "Initial number of preys: " var: nb_preys_init category: "Prey" ;
   parameter "Prey max energy: " var: prey_max_energy category: "Prey" ;
   parameter "Prey max transfer: " var: prey_max_transfer  category: "Prey" ;
   parameter "Prey energy consumption: " var: prey_energy_consum  category: "Prey" ;
   output {
      display main_display {
         grid vegetation_cell lines: rgb("black") ;
         species prey aspect: base ;
      }
   }
}
```