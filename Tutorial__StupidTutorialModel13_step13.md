# 13. Charts
Show how to add a simple time series graph to a model. This graph is important for understanding results now that reproduction and mortality change the abundance of bugs.







## Formulation
No change is made to the model formulation. A graph is added to display the number of bugs alive at each time step.





## Model Definition


We previously defined a histogram output, the time series one follows the same structure. We simplify change the **`type`** of chart. Note that we chose here to give a blue color to our serie.

```
output {
    ...
    display series_display {
	  chart "Population history" type: series  {
	        data "Bugs" value: length(bug) color: #blue;            
	   }
    }
}
```




## Complete Model

```
model StupidModel13

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
                        data "[9;10]" value: bug count (each.size > 9) color: #red;	           }
	      }
              display series_display {
	          chart "Population history" type: series  {
	              data "Bugs" value: length(bug) color: #blue;            
	           }
    	     }
	}
}
```