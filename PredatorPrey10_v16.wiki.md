
<br />
# <font color='blue'>Purpose</font>

Illustrate how to define charts

# <font color='blue'>Formulation</font>
  * Adding a new display to visualize:
    * A chart representing the evolution of the quantity of prey and predator agents over the time
    * Two histograms representing the energy distribution of the prey and predator agents



# <font color='blue'>Model</font>

## Output

GAMA can display various chart types:
  * Time series
  * Pie charts
  * Histograms

A chart must be defined in a display : it behaves exactly like any other layer.
Definition of a chart :

```
chart chart_name type: chart_type  {
     [data]
}
```

The data to draw are define inside the chart block:

```
     data data_legend value: data_value
```

We add a new display called **Population\_information** refresh every 5 simulation steps.
Inside this display, we define 3 charts: one of type _series_, two of type _histogram_ :
  * "Species evolution"; background : white; size : {1, 0.4}; position : {0, 0.05}
    * data1: number\_of\_preys; color : blue
    * data2: number\_of\_predator; color : red

  * "Prey Energy Distribution"; background : lightGray; size : {0.5, 0.4}; position : {0, 0.5}
    * data "]0;0.25]" : number of preys with (each.energy <= 0.25) ;
    * data "]0.25;0.5]" number of preys with ((each.energy > 0.25) and (each.energy <= 0.5)) ;
    * data "]0.5;0.75]" number of preys with ((each.energy > 0.5) and (each.energy <= 0.75)) ;
    * data "]0.75;1]" number of preys with  (each.energy > 0.75) ;

  * "Predator Energy Distribution"; background : lightGray; size : {0.5, 0.4}; position : {0.5, 0.5}
    * data "]0;0.25]" : number of predators with (each.energy <= 0.25) ;
    * data "]0.25;0.5]" number of predators with ((each.energy > 0.25) and (each.energy <= 0.5)) ;
    * data "]0.5;0.75]" number of predators with ((each.energy > 0.5) and (each.energy <= 0.75)) ;
    * data "]0.75;1]" number of predators with  (each.energy > 0.75) ;

To evaluate the value of the data of the two histogram, we use the operator **list count condition" that returns the number of elements of**list**for which the condition is true.**

```
     display Population_information refresh_every: 5 {
         chart "Species evolution" type: series background: rgb("white") size: {1,0.4} position: {0, 0.05} {
            data "number of preys" value: nb_preys color: rgb("blue") ;
            data "number of predators" value: nb_predators color: rgb("red") ;
         }
         chart "Prey Energy Distribution" type: histogram background: rgb("lightGray") size: {0.5,0.4} position: {0, 0.5} {
            data "]0;0.25]" value: prey count (each.energy <= 0.25) ;
            data "]0.25;0.5]" value: prey count ((each.energy > 0.25) and (each.energy <= 0.5)) ;
            data "]0.5;0.75]" value: prey count ((each.energy > 0.5) and (each.energy <= 0.75)) ;
            data "]0.75;1]" value: prey count (each.energy > 0.75) ;
         }
         chart "Predator Energy Distribution" type: histogram background: rgb("lightGray") size: {0.5,0.4} position: {0.5, 0.5} {
            data "]0;0.25]" value: predator count (each.energy <= 0.25) ;
            data "]0.25;0.5]" value: predator count ((each.energy > 0.25) and (each.energy <= 0.5)) ;
            data "]0.5;0.75]" value: predator count ((each.energy > 0.5) and (each.energy <= 0.75)) ;
            data "]0.75;1]" value: predator count (each.energy > 0.75) ;
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
   reflex stop_simulation when: (nb_preys = 0) or (nb_predators = 0) {
      do halt ;
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
         do choose_cell ;
         location <- myCell.location ;
      }
      action choose_cell ;
      
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
      action choose_cell {
         myCell <- (myCell.neighbours) with_max_of (each.food);
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
      
      action choose_cell {
         vegetation_cell myCell_tmp <- shuffle(myCell.neighbours) first_with (!(empty (prey inside (each))));
         if myCell_tmp != nil {
            myCell <- myCell_tmp;
         } else {
            myCell <- one_of (myCell.neighbours);
         } 
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
      display Population_information refresh_every: 5 {
         chart "Species evolution" type: series background: rgb("white") size: {1,0.4} position: {0, 0.05} {
            data "number of preys" value: nb_preys color: rgb("blue") ;
            data "number of predators" value: nb_predators color: rgb("red") ;
         }
         chart "Prey Energy Distribution" type: histogram background: rgb("lightGray") size: {0.5,0.4} position: {0, 0.5} {
            data "]0;0.25]" value: prey count (each.energy <= 0.25) ;
            data "]0.25;0.5]" value: prey count ((each.energy > 0.25) and (each.energy <= 0.5)) ;
            data "]0.5;0.75]" value: prey count ((each.energy > 0.5) and (each.energy <= 0.75)) ;
            data "]0.75;1]" value: prey count (each.energy > 0.75) ;
         }
         chart "Predator Energy Distribution" type: histogram background: rgb("lightGray") size: {0.5,0.4} position: {0.5, 0.5} {
            data "]0;0.25]" value: predator count (each.energy <= 0.25) ;
            data "]0.25;0.5]" value: predator count ((each.energy > 0.25) and (each.energy <= 0.5)) ;
            data "]0.5;0.75]" value: predator count ((each.energy > 0.5) and (each.energy <= 0.75)) ;
            data "]0.75;1]" value: predator count (each.energy > 0.75) ;
         }
      }
   }
}
```