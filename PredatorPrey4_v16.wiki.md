
<br />
# <font color='blue'>Purpose</font>

Illustrate how to define a monitor and how to use inspectors.

# <font color='blue'>Formulation</font>
  * Adding of a monitor to follow the evolution of the number of prey agents

# <font color='blue'>Model</font>

## Global variable
We add a new global variable:
  * **nb\_preys** : returns, each time is called, the current number of prey agents

To allow a variable to be computed each time it is called, we have to use the **->{expression}** facet.
We use as well the operator **length** that returns the number of elements in a list.

Thus, In the global section, we add the **nb\_preys** global variable:
```
   int nb_preys -> {length (prey)};
```

## Monitor
A monitor allows to follow the value of an arbitrary expression in GAML. It has to be defined in an output section. A monitor is defined as follows:
```
      monitor monitor_name value: an_expression refresh_every: nb_steps;
```

With:
  * value: mandatory, its value will be displayed in the monitor.
  * refresh\_every: int, optional : number of simulation steps between two computations of the expression (default is 1).

In this model, we define a monitor to follow the value of the variable **nb\_preys**:
```
      monitor "number of preys" value: nb_preys;
```

## Inspector

Inspectors allow to obtain informations about a species or an agent. There are two kinds of agent information features:
  * Species browser: provides informations about all the agents of a species. Available in the Agents menu.

![http://gama-platform.googlecode.com/files/browser_table.png](http://gama-platform.googlecode.com/files/browser_table.png)


  * Agent inspector: provides information about one specific agent. Also allows to change the values of its variables during the simulation. Available from the Agents menu, by right\_clicking on a display, in the species inspector or when inspecting another agent. It provides also the possibility to «highlight» the inspected agent.

![http://gama-platform.googlecode.com/files/inspector.png](http://gama-platform.googlecode.com/files/inspector.png)


# <font color='blue'>Complete model</font>

```
model prey_predator

global {
   int nb_preys_init <- 200 min: 1 max: 1000 ;
   float prey_max_energy <- 1.0;
   float prey_max_transfer <- 0.1;
   float prey_energy_consum <- 0.05;
   int nb_preys -> {length (prey)};
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
      monitor "number of preys" value: nb_preys;
      display main_display {
         grid vegetation_cell lines: rgb("black") ;
         species prey aspect: base ;
      }
   }
}
```