
<br />
# <font color='blue'>Purpose</font>

Illustrate how to define complex aspects.

# <font color='blue'>Formulation</font>
  * Definition of two new aspects for the prey and predator agents:
    * A icon
    * A square with information about the agent energy

  * Use of the **icon** aspect as default aspect for the prey and predator agents.

# <font color='blue'>Model</font>

## Parent species

We add a new variable of type _string_ called **my\_icon** to the **generic\_species**.
We define as well two new aspects:
  * **icon** : draw the image given by the variable **icon**
  * **info** : draw a square of side size **size** and color **color**; draw as a text the energy of the agent (with a precision of 2)

```
   species generic_species {
      ...
      const my_icon type: file;
      ...
      aspect base {
         draw circle(size) color: color ;
      }
      aspect icon {
         draw my_icon size: 2 * size ;
      }
      aspect info {
         draw square(size) color: color ;
         draw string(energy with_precision 2) size: 3 color: rgb("black") ;
      }
   }
```

## Prey species
We specialize the **prey** species from the **generic\_species** species:
  * definition of the initial value of the agent variables
```
   species prey parent: generic_species {
      ...  
      const my_icon type: file <- file("../includes/data/predator_prey_sheep.png") ;
      ...
   }
```

The image file is here: ![http://gama-platform.googlecode.com/files/predator_prey_sheep.png](http://gama-platform.googlecode.com/files/predator_prey_sheep.png)

You have to copy it in your project folder: includes/data/

## Predator species
As done for the **prey** species, we specialize the **predator** species from the **generic\_species** species:
  * definition of the initial value of the agent variables

```
   species predator parent: generic_species {
      ...
      const my_icon type: file <- file("../includes/data/predator_prey_wolf.png") ;
      ...
   }
```

The image file is here: ![http://gama-platform.googlecode.com/files/predator_prey_wolf.png](http://gama-platform.googlecode.com/files/predator_prey_wolf.png)

You have to copy it in your project folder: includes/data/

## Display
We change the default aspect of the prey and predator agents to **icon** aspect.
```
   output {
      display main_display {
         grid vegetation_cell lines: rgb("black") ;
         species prey aspect: icon ;
         species predator aspect: icon ;
      }
   }
```

We define a new display called info\_display that displays the prey and predator agents with the **info** aspect.
```
   output {
      display info_display {
         species prey aspect: info;
         species predator aspect: info;
      }
   }
```
# <font color='blue'>Complete model</font>

```
model prey_predator

global {
   int nb_preys_init <- 200 min: 1 max: 1000 ;
   float prey_max_energy <- 1.0;
   float prey_max_transfer <- 0.1;
   float prey_energy_consum <- 0.05;
   int nb_preys -> {length (prey)};
   int nb_predators_init <- 20 min: 0 max: 200;
   float predator_max_energy <- 1.0;
   float predator_energy_transfer <- 0.5;
   float predator_energy_consum <- 0.02;
   int nb_predators -> {length (predator)};
   float prey_proba_reproduce <- 0.01;
   int prey_nb_max_offsprings <- 5; 
   float prey_energy_reproduce <- 0.5; 
   float predator_proba_reproduce <- 0.01;
   int predator_nb_max_offsprings <- 3;
   float predator_energy_reproduce <- 0.5;
   init {
      create prey number: nb_preys_init ;
      create predator number: nb_predators_init ;
   }
}
entities {
   species generic_species {
      const size type: float <- 1.0 ;
      const color type: rgb <- rgb("blue") ;
      const max_energy type: float <- prey_max_energy ;
      const max_transfer type: float <- prey_max_transfer ;
      const energy_consum type: float <- prey_energy_consum ;
      const proba_reproduce type: float ;
      const nb_max_offsprings type: int ;
      const energy_reproduce type: float ;
      vegetation_cell myCell <- one_of (vegetation_cell) ;
      float energy <- (rnd(1000) / 1000) * max_energy  update: energy - energy_consum max: max_energy ;
      const my_icon type: file;
      init {
         location <- myCell.location;
      }
      reflex basic_move {
         myCell <- one_of (myCell.neighbours) ;
         location <- myCell.location ;
      }
      reflex die when: energy <= 0 {
         do die ;
      }
      reflex reproduce when: (energy >= energy_reproduce) and (flip(proba_reproduce)) {
         int nb_offsprings <- 1 + rnd(nb_max_offsprings -1);
         create species(self) number: nb_offsprings {
            myCell <- myself.myCell ;
            location <- myCell.location ;
            energy <- myself.energy / nb_offsprings ;
         }
         energy <- energy / nb_offsprings ;
      }
      aspect base {
         draw circle(size) color: color ;
      }
      aspect icon {
         draw my_icon size: 2* size ;
      }
      aspect info {
         draw square(size) color: color ;
         draw string(energy with_precision 2) size: 3 color: rgb("black") ;
      }
   }

   species prey parent: generic_species {
      const color type: rgb <- rgb("blue") ;
      const max_energy type: float <- prey_max_energy ;
      const max_transfer type: float <- prey_max_transfer ;
      const energy_consum type: float <- prey_energy_consum ;
      const proba_reproduce type: float <- prey_proba_reproduce ;
      const nb_max_offsprings type: int <- prey_nb_max_offsprings ;
      const energy_reproduce type: float <- prey_energy_reproduce ;
      const my_icon type: file <- file("../includes/data/predator_prey_sheep.png") ;
      
      reflex eat when: myCell.food > 0 {
         float energy_transfer <- min([max_transfer, myCell.food]) ;
         myCell.food <- myCell.food - energy_transfer ;
         energy <- energy + energy_transfer ;
      }
   }

   species predator parent: generic_species {
      const color type: rgb <- rgb("red") ;
      const max_energy type: float <- predator_max_energy ;
      const energy_transfer type: float <- predator_energy_transfer ;
      const energy_consum type: float <- predator_energy_consum ;
      const proba_reproduce type: float <- predator_proba_reproduce ;
      const nb_max_offsprings type: int <- predator_nb_max_offsprings ;
      const energy_reproduce type: float <- predator_energy_reproduce ;
      list<prey> reachable_preys update: (prey inside(myCell));
      const my_icon type: file <- file("../includes/data/predator_prey_wolf.png") ;
      
      
      reflex eat when: ! empty(reachable_preys) {
       	ask one_of (reachable_preys) {
            do die ;
         }
         energy <- energy + energy_transfer ;
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
   parameter "Initial number of predators: " var: nb_predators_init category: "Predator" ;
   parameter "Predator max energy: " var: predator_max_energy category: "Predator" ;
   parameter "Predator energy transfer: " var: predator_energy_transfer  category: "Predator" ;
   parameter "Predator energy consumption: " var: predator_energy_consum  category: "Predator" ;
   parameter "Prey probability reproduce: " var: prey_proba_reproduce category: "Prey" ;
   parameter "Prey nb max offsprings: " var: prey_nb_max_offsprings category: "Prey" ;
   parameter "Prey energy reproduce: " var: prey_energy_reproduce category: "Prey" ;
   parameter "Predator probability reproduce: " var: predator_proba_reproduce category: "Predator" ;
   parameter "Predator nb max offsprings: " var: predator_nb_max_offsprings category: "Predator" ;
   parameter "Predator energy reproduce: " var: predator_energy_reproduce category: "Predator" ;
   output {
      monitor "number of preys" value: nb_preys;
      monitor "number of predators" value: nb_predators;
      display main_display {
         grid vegetation_cell lines: rgb("black") ;
         species prey aspect: icon ;
         species predator aspect: icon ;
      }
   }
}
```