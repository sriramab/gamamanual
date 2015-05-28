# 12. Bug Reproduction
So far, our bugs population was fixed, no agent were created or deleted during simulation (all the bugs were created during the initialization process). In the present step we will show you to create new agent and discard existing ones during simulation.








## Formulation
  * When a bug's size reaches 10, it reproduces by splitting into 5 new bugs. Each new bug has an initial size of 0.0, and the old bug disappears.
  * New bugs are placed at the first empty location randomly selected within +/- 3 cells of their parent's last location. If no location is identified within 5 random draws, then the newly created bug dies.
  * A new bug parameter, **survivalProbability**, is initialized to 0.95. Each time step, each bug draws a uniform random number, and if it is greater than survivalProbability, the bug dies and is dropped.
  * This mortality action is scheduled after the bug moves and grows.
  * The model stopping rule is changed: the model stops after 1000 time steps have been executed or when the number of bugs reaches zero.






## Model Definition

### new neighborhood for the cells
As in the context of the reproduction behavior of the bug agents, we will need to compute the neighborhood at a distance of 3, we add a new variable to the cells. Note the interest of defining such variable is for optimization purpose (to avoid useless re-computation).
```
grid cell width: 100 height: 100 neighbours: 4 {
	...
        list<cell> neighbours3 <- self neighbours_at 3;
	...
}
```
### introducing survivability

We have to introduce a new variable `survivalProbability`, we will set it at 0.95. We will also define a reflex that will manage the death of agents using this parameter. Killing an agent is done by using the **die** action.

```
species bug schedules: bug sort_by ( - each.size){
	...
        float survivalProbability <- 0.95;
	
        ...
	reflex dying when: not flip(survivalProbability) {
    	    do die;
        }
	...
} 
```

Note the use of the **flip(proba)** operator that test a probability: it draws an random number between 0 and 1 and if this number is lower than the probe, it returns true; false otherwise.

### multiplying

As we saw, to make an agent dies and create new agent is pretty easy, it is done with the **`create`** statement and the **`die`** action. We will do it within a new reflex.

```
species bug schedules: bug sort_by ( - each.size){
	 ...
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
} 
```


### changing the stop condition

We have to modify the `shouldHalt` reflex as follow:

```
global torus: true{
        ...
	reflex shouldHalt when: cycle = 999 or empty(bug)  {
		 do halt;
        }
}
```





## Complete Model
_Nota bene: we updated the histograms to show the 10 classes of size between 0 and 10 as once a bug reaches 10 it will be replaced by new smaller agents_
```
model StupidModel12

global torus: true{
	int numberBugs <- 100;
        float globalMaxConsumption <- 1.0;
        float globalMaxFoodProdRate <- 0.01;
    
	init {
		create bug number: numberBugs {
			my_place <- one_of(cell);
			location <- my_place.location;
		}
	}
	reflex shouldHalt when: cycle = 999 or empty(bug)  {
		 do halt;
        }
	reflex write_results {
		save [cycle,bug min_of each.size, mean (bug collect each.size),bug max_of each.size] type: "csv" to: "result.csv";
	}
	
}

grid cell width: 100 height: 100 neighbours: 4 {
	list<cell> neighbours4 <- self neighbours_at 4;
	list<cell> neighbours3 <- self neighbours_at 3;
	float maxFoodProdRate <- globalMaxFoodProdRate;
	float foodProd <- (rnd(1000) / 1000) * maxFoodProdRate;
	float food <- 0.0 update: food + foodProd ;
}

species bug schedules: bug sort_by ( - each.size){
	cell my_place;
	float size <- 1.0;
	float maxConsumption <- globalMaxConsumption;
	float survivalProbability <- 0.95;
	reflex basic_move {
		cell destination <- (my_place.neighbours4 where empty(each.agents) + my_place) with_max_of (each.food);
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

experiment stupidModel type: gui {
	parameter "numberBugs" var: numberBugs;
 	parameter "globalMaxConsumption" var: globalMaxConsumption;
  	parameter "globalMaxFoodProdRate" var: globalMaxFoodProdRate;	
  	output {
		display stupid_display {
			grid cell;
			species bug aspect: basic;
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
                        data "[9;10]" value: bug count (each.size > 9) color: #red;	            }
	       }
	}
}
```