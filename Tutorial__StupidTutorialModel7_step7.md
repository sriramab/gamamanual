# 7. Simulation Stopping
In the present model we will show you how to stop automatically once a condition is met and how to _clean up_ once the model is stopped.


<br />

---


## Formulation
  * The model stops when the largest bug reaches a size of 100.
<br />

---

## Model Definition
### using a world reflex
The whole system is what we call the **World** (**`global`** section). Thus, it makes sense that the world has to stop the execution of the simulation by using the specific **`halt`** action. We would do that by adding the following statement in the global section of our model:

```
global {
    ...
    reflex stop_simulation when: (bug first_with (each.size >= 100)) != nil {
	do action: halt;
    }
}
```

We can see that:
  * The world can have reflexes that are defined in the same way as normal agents
  * It is possible to add a condition to the execution of a reflex using the **`when`** parameter
  * We could have used the **`pause`** command instead of the **`halt`** one (in order to resume manually the execution of the simulation).

### using bugs reflex
Instead of defining a reflex within the **global** section (i.e. **world** level), we could also have define a reflex within the bugs. Once a bug reaches the size of '100', it will **`ask`** the world to stop. This can be done as follows :

```
entities {
    species bug {
	...
	reflex askToHalt when: (size>=100) {
    	    ask world {
		do halt;
	    }
	}
    }
}
```

  * For the first time we see the **`ask`** command here. As it sounds, it allows an agent to ask (understand to force) an agent to execute something.
  * Note that **`world`** represents the world agent.


<br />

---

## Complete Model

```
model StupidModel7

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

species bug {
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