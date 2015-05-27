# 10. Sorted Actions
The present model shows how to sort a list of agents, and cause an agent action to be executed in the order based on the bug's size.


<br />

---


## Formulation
  * The bug execution is un-randomized so it is executed in descending size order.

<br />

---

## Model Definition
Generally, the schedule with respect to which agents execute their action is randomized by a shuffle each time step. However, GAMA offers the possibility for the modeler to specify the scheduling strategy. In our context, we just have to use the **`schedules`** of species in order to consider the agent size.

```
species bug schedules: bug sort_by ( - each.size){
      ...
}	
```

Note that we used the **list sort\_by expression** operator to sort the bug list according to their size (from the biggest to the smallest).

<br />

---

## Complete Model

```
model StupidModel10
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
	reflex write_results {
		save [cycle,bug min_of each.size, mean (bug collect each.size),bug max_of each.size] type: "csv" to: "result.csv";
	}
	reflex stop_simulation when: (bug first_with (each.size >= 100)) != nil {
               do halt;
       }
}

grid cell width: 100 height: 100 neighbours: 4 {
	list<cell> neighbours4 <- self neighbours_at 4;
	float maxFoodProdRate <- globalMaxFoodProdRate;
	float foodProd <- (rnd(1000) / 1000) * maxFoodProdRate;
	float food <- 0.0 update: food + foodProd ;
}

species bug schedules: bug sort_by ( - each.size){
	cell my_place;
	float size <- 1.0;
	float maxConsumption <- globalMaxConsumption;
	reflex basic_move {
		cell destination <- shuffle(my_place.neighbours4) first_with empty(each.agents);
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
	                data "[0;10]" value: bug count (each.size < 10) color: #red;
	                data "[10;20]" value: bug count ((each.size > 10) and (each.size < 20)) color:#red;
	                data "[20;30]" value: bug count ((each.size > 20) and (each.size < 30)) color:#red;
	                data "[30;40]" value: bug count ((each.size > 30) and (each.size < 40)) color:#red;
	                data "[40;50]" value: bug count ((each.size > 40) and (each.size < 50)) color:#red;
	                data "[50;60]" value: bug count ((each.size > 50) and (each.size < 60)) color:#red;
	                data "[60;70]" value: bug count ((each.size > 60) and (each.size < 70)) color:#red;
	                data "[70;80]" value: bug count ((each.size > 70) and (each.size < 80)) color:#red;
	                data "[80;90]" value: bug count ((each.size > 80) and (each.size < 90)) color:#red;
	                data "[90;100]" value: bug count (each.size > 90) color: #red;
	           }
	      }
	}
}
```