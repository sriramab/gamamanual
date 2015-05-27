# 16. Predators
So far we have considered only bugs agent wandering around an environment. Now, we add a new species called "predators" that will hunt bugs. It will allow us to present how agent of different species can interact.
_Nota bene_: it would be possible to define a parent species that would consist of common behavior between the 2 species, please see [step 5](Tutorial__PredatorPreyTutorial_step5.md) of the prey-predator tutorial on how to do so.


<br />

---


## Formulation
  * 200 predator objects are intialized and randomly distributed as the bugs are. A cell can contain a predator as well as a bug. Predators are created after bugs are.
  * Predators have one method: hunt. First, a predator looks through a shuffled list of its immediately neighboring cells (including its own cell). As soon as the predator finds a bug in one of these cells it kills the bug and moves into the cell. (However, if the cell already contains a predator, the hunting predator simply quits and remains at its current location.) If these cells contain no bugs, the predator moves randomly to one of them.
  * Predator hunting is scheduled after all the bug actions.
<br />

---

## Model Definition
### defining predators
Similar to the definition of the move reflex in the first model, we define a hunt reflex for the predators. Although, this reflex is a bit more complex as you may see below:

```
species predator schedules:[]{
	cell my_place;             
        
        reflex hunt {
    	     list<cell> neighbour_cells <- my_place neighbours_at 1;
             bug chosen_prey <- one_of((neighbour_cells + my_place) accumulate (each.agents of_species bug));
       	     if chosen_prey != nil {
                    cell new_place <- chosen_prey.my_place;    
                    if empty(new_place.agents of_species predator){
            	           my_place <- new_place;
                           location <- new_place.location;
                           ask chosen_prey {
                                 do die;
                           } 
                    }
              } else {
                   my_place <- one_of(neighbour_cells);
                   location <- my_place.location;
              }
        }
                
        aspect basic{
             draw circle(0.5) color: #blue;
        }
} 
```

**Explanations:**
  * We select cells around the predator (direct neighbourhood)
  * We select the bugs contained inside these cells
  * We select one of them randomly.
  * If we have a chosen prey.
    * We check it's empty of other predators.
      * If so we go there and kill the bug.
      * If there is another predator already, nothing happens.
  * If we have no place with a bug.
    * We move randomly in a neighbour cell.

### scheduling Predators

The scheduler that we want to achieve is a bit more complex as well. The simplest solution is to create a new species dedicated to the scheduling and remove the other species from the global scheduler.

Definition of the scheduler species
```
species scheduler schedules: cell + (bug sort_by ( - each.size)) + shuffle(predator);
```

Removing of the other species from the global scheduler by setting **schedules** to a empty list:
```
grid cell width: width height: height neighbours: 4 schedules:[]{
...
}

species bug schedules:[]{
...
}

species predator schedules:[]{
...
}
```
### instantiating predators

Similarly to the creation of bugs in the first model, we create the predators in the init section of the world as follows:

```
global {
    ...
    init {
		...
                create predator number: 200 {	
			my_place <- one_of(cell);
			location <- my_place.location;
		}
		...
     }
```

### visualization
We have to add the predator species to the stupid\_display:

```
display stupid_display {
    grid stupid_grid;
    species bug aspect: basic;
    species predator aspect: basic;
}
```

For convenience, we also add an input to the chart output:
```
display series_display {
	        chart "Population history" type: series  {
	            ...
                    data "Predators" value: length(predator) color: #red;            
	        }
            }
```


<br />

---

## Complete Model

```
model StupidModel16

global {
    int numberBugs <- 100;
    float globalMaxConsumption <- 1.0;
    float globalMaxFoodProdRate <- 0.01;
    float initialBugSizeMean <- 0.1;
    float initialBugSizeSD <- 0.03;
    matrix<float> init_data <- matrix<float>(csv_file("../data/Stupid_Cell.Data", "\t"));
    int width <- int(max (copy_between(init_data column_at 0,3, init_data.rows - 1)));
    int height  <- int(max(copy_between(init_data column_at 1, 3,init_data.rows - 1)));
    geometry shape <- rectangle(width,height);
    init {
		create bug number: numberBugs {
			my_place <- one_of(cell);
			location <- my_place.location;
		}
                create predator number: 200 {	
			my_place <- one_of(cell);
			location <- my_place.location;
		}
		loop i from: 3 to: ((init_data.rows)) - 1 {
			int ind_i <- int(init_data[0,i]); 
			int ind_j <- int(init_data[1,i]);
			ask cell [ind_i,ind_j] {
				foodProd <- init_data[2,i];
			}  
		} 
     }
     reflex shouldHalt when: cycle = 999 or empty(bug)  {
		 do halt;
     }
     reflex write_results {
		save [cycle,bug min_of each.size, mean (bug collect each.size),bug max_of each.size] type: "csv" to: "result.csv"; 
     }
	
}
species scheduler schedules: cell + (bug sort_by ( - each.size)) + shuffle(predator);

grid cell width: width height: height neighbours: 4 schedules:[]{
	list<cell> neighbours4 <- self neighbours_at 4;
	list<cell> neighbours3 <- self neighbours_at 3;
	float maxFoodProdRate <- globalMaxFoodProdRate;
	float foodProd <- (rnd(1000) / 1000) * maxFoodProdRate;
	float food <- 0.0 update: food + foodProd;
	rgb color <- rgb(0, min([255, int(food * 255 *2)]), 0) update: rgb(0,min([255, int(food * 255 * 2)]), 0);
}

species bug schedules:[]{
	cell my_place;
	float size <- max([0,gauss(initialBugSizeMean,initialBugSizeSD)]);
	float maxConsumption <- globalMaxConsumption;
	float survivalProbability <- 0.95;
	reflex basic_move {
		cell destination <- shuffle(my_place.neighbours4 where empty(each.agents) + my_place) with_max_of (each.food);
		if (destination != nil) {
			my_place <- destination;
			location <- destination.location;
		}
	}
	reflex grow {
		float transfer <- min([my_place.food,maxConsumption]);
		size <- size + transfer;
		my_place.food <- my_place.food - transfer;
	}
	reflex dying when: not flip(survivalProbability) {
    	     do die;
        }
	reflex reproduce when: size >= 10 {
		list<cell> possible_nests <- my_place.neighbours3 where empty(each.agents);
         	create bug number: 5 {
                     cell nest <- one_of(possible_nests);
                     if condition: nest != nil {
                       	 remove nest from: possible_nests;
            	         my_place <- nest;
                	 location <- nest.location;
            	         size <- 0.0;
                     } else {
                	do die;
                     }
                }
               do die;
        }
	aspect basic {
		int val <- int(255 * (1 - min([1.0,size/10.0])));
		draw circle(0.5) color: rgb(255,val,val);
	}
} 

species predator schedules:[]{
	cell my_place;             
    reflex hunt {
    	list<cell> neighbour_cells <- my_place neighbours_at 1;
        bug chosen_prey <- one_of((neighbour_cells + my_place) accumulate (each.agents of_species bug));
       	if chosen_prey != nil {
            cell new_place <- chosen_prey.my_place;    
            if empty(new_place.agents of_species predator){
            	my_place <- new_place;
                location <- new_place.location;
                ask chosen_prey {
                   do die;
                } 
            }
        }
        else {
            my_place <- one_of(neighbour_cells);
            location <- my_place.location;
        }
    }
                
    aspect basic{
        draw circle(0.5) color: #blue;
    }
} 


experiment stupidModel type: gui {
	parameter "numberBugs" var: numberBugs;
 	parameter "globalMaxConsumption" var: globalMaxConsumption;
  	parameter "globalMaxFoodProdRate" var: globalMaxFoodProdRate;	
  	parameter "initialBugSizeMean" var: initialBugSizeMean;
  	parameter "initialBugSizeSD" var: initialBugSizeSD;
	
  	output {
		display stupid_display {
			grid cell;
			species bug aspect: basic;
			species predator aspect: basic;
		}
		display histogram_display {
	            chart "Size distribution" type: histogram {
                        data "[0;1]" value: bug count (each.size < 1) color: #red;
                        data "[1;2]" value: bug count ((each.size > 1) and (each.size < 2)) color:#red;
                        data "[2;3]" value: bug count ((each.size > 2) and (each.size < 3)) color:#red;
                        data "[3;4]" value: bug count ((each.size > 3) and (each.size < 4)) color:#red;
                        data "[4;5]" value: bug count ((each.size > 4) and (each.size < 5)) color:#red;
                        data "[5;6]" value: bug count ((each.size > 5) and (each.size < 6)) color:#red;
                        data "[6;7]" value: bug count ((each.size > 6) and (each.size < 7)) color:#red;
                        data "[7;8]" value: bug count ((each.size > 7) and (each.size < 8)) color:#red;
                        data "[8;9]" value: bug count ((each.size > 8) and (each.size < 9)) color:#red;
                        data "[9;10]" value: bug count (each.size > 9) color: #red;
	        }
	    }
	    display series_display {
	        chart "Population history" type: series  {
	            data "Bugs" value: length(bug) color: #blue;            
                    data "Predators" value: length(predator) color: #red;            
	        }
            }
	}
}
```