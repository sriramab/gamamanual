# 5. Parameters
In the present step we will make certain global variables available in the simulation UI as parameters (parameter settings tab).


<br />

---


## Formulation
Make these variables into parameters that can be accessed through the settings window:
  * Initial number of bugs (a model parameter)
  * The maximum daily food consumption (a bug parameter)
  * The maximum food production (a cell parameter).
<br />

---

## Model Definition
### parameter definition
  * We introduce the variables setting with this model. To do so, we add the **`parameter`** statement in the experiment section. At least, a parameter is a name (a string) and a global variable (_var: variable\_name_)):

```
experiment stupidModel type: gui {
	parameter "numberBugs" var: numberBugs;
 	...
}
```

  * Parametrization is only available to the world's variable within the global section. Thus for bugs' and cells' parameters, we have to define global variables that will be used in the their personal variable definition. We add the following statement to the global section:

```

global torus: true{
	...
	float globalMaxConsumption <- 1.0;
	float globalMaxFoodProdRate <- 0.01;
        ...
```

  * We change the `maxFoodProdRate`variable definition within cells like this:

```
grid cell width: 100 height: 100 neighbours: 4 {
	...
	float maxFoodProdRate <- globalMaxFoodProdRate;
	...
}
```

  * We also change the `maxConsumption` variable definition within bugs like this:

```
species bug {
      ...
      float maxConsumption <- globalMaxConsumption;
      ...
```


  * At last, we add the new parameters in the experiment:
```
experiment stupidModel type: gui {
	...
 	parameter "globalMaxConsumption" var: globalMaxConsumption;
  	parameter "globalMaxFoodProdRate" var: globalMaxFoodProdRate;	
  	...
}
```

### Nota Bene
  * It seems useless to declare a `maxFoodProdRate` variable, but in the case we want heterogeneous values of `maxFoodProdRate`, it will be very easily done.

<br />

---

## Complete Model

```
model StupidModel5

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
		draw circle(size) color: rgb(255,val,val);
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
	}
}
```