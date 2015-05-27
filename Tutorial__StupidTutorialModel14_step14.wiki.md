# 14. Random Normal Init
In the present model, we introduce the use of random number distribution. A common use for them is to add variability among initial individuals.


<br />

---


## Formulation
  * Two new model parameters are added, and put on the parameter settings window: _initialBugSizeMean_ and _initialBugSizeSD_. Values of these parameters are 0.1 and 0.03.
  * Instead of initializing bug sizes to 1.0 (Sect. 2.2), sizes are drawn from a gaussian (normal) distribution defined by _initialBugSizeMean_ and _initialBugSizeSD_.
  * Negative values are very likely to be drawn from normal distributions such as the one used here. To avoid them, a check is introduced to limit initial bug size to a minimum of zero.


<br />

---

## Model Definition
### adding new parameters
You already know how to add variables and make them parameters.

First, we add new global variables:
```
global torus: true{
	...
    	float initialBugSizeMean <- 0.1;
	float initialBugSizeSD <- 0.03;
}
```

Then, we add new parameters in the experiment:
```
experiment stupidModel type: gui {
	...	
  	parameter "initialBugSizeMean" var: initialBugSizeMean;
  	parameter "initialBugSizeSD" var: initialBugSizeSD;
}
```
### normal randomization of bug size

In order to use a gaussian distribution, we simply have to use the dedicated operator: **`gauss`** with values of the mean (`initialBugSizeMean`) and of the standard deviation (`initialBugSizeSD`). In addition, we use the **max** operator (with 0) to be sure to get a positive value.

```
species bug schedules: bug sort_by ( - each.size){
	...
	float size <- max([0,gauss(initialBugSizeMean,initialBugSizeSD)]);
        ...
}
```

Note that other operators exist to represent other random distribution (e.g. [Poisson distribution](G__OperatorsLZ#poisson.md))

<br />

---

## Complete Model

```
model StupidModel14

global torus: true{
	int numberBugs <- 100;
   	float globalMaxConsumption <- 1.0;
    	float globalMaxFoodProdRate <- 0.01;
    	float initialBugSizeMean <- 0.1;
	float initialBugSizeSD <- 0.03;
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
	float food <- 0.0 update: food + foodProd;
}

species bug schedules: bug sort_by ( - each.size){
	cell my_place;
	float size <- max([0,gauss(initialBugSizeMean,initialBugSizeSD)]);
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
  	parameter "initialBugSizeMean" var: initialBugSizeMean;
  	parameter "initialBugSizeSD" var: initialBugSizeSD;
	
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
                        data "[9;10]" value: bug count (each.size > 9) color: #red;	        }
	    }
	    display series_display {
	        chart "Population history" type: series  {
	            data "Bugs" value: length(bug) color: #blue;            
	        }
    	    }
	}
}
```