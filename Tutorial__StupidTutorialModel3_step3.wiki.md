# 3. Habitat Cells
Here, we give a behavior to the grid cells. It also illustrates how agents and cells interact.


<br />

---


## Formulation
  * The grid cells have now instance variables for their food availability, a maximum food production rate and the actual food production. Cells also have a variable for reference of the bug at their location.
  * Food availability is initialized to 0.0, and maximum food production rate is initialized to 0.01. At each time step, food availability is increased by a food production variable. This variable is a random floating point number  zero and the food production rate.
  * The bug growth corresponds to the food consumption. Food consumption is equal to the minimum of (a) the bug's maximum consumption rate (set to 1.0) and (b) the bug cell food availability.
  * The food consumed by each bug is subtracted from the food availability of its cell.
<br />

---

## Model Definition

### giving a behavior to the cells
Here, we have to add the following variables to the cells in the grid section: `maximum food production rate`, `food availability` and `food production`.

```
grid cell width: 100 height: 100 neighbours: 4 {
	...
	float maxFoodProdRate <- 0.01;
	float foodProd <- (rnd(1000) / 1000) * maxFoodProdRate;
	float food <- 0.0;
}
```

The random operator works only on integer but allows us to set the precision. In this example, we have a precision of 10^-3 (as we use a range from 0 to 1000) and generate a number in the `[0;0.001]` range.

### increasing cell's food
Since we already defined the required variables, we can now update them at each time step, either using a reflex or using the automatic update (`value` parameter).

```
float food <- 0.0 update: food + foodProd;
```

In the `update` parameter, which is evaluated at each time step, we add the previously available food and the `foodProd` variable (which is updated at each time step thanks to `update` parameter too).

### bug growth
Instead of having a constant increase, we now want to have a dynamic one. The increase is defined as the minimum of `maxConsumption` (bug's variable to define) and `food` (current cell's variable). Note that this quantity has to be subtracted from the cell as it is "consumed" by the bug...
Since many parameters are involved, the growth is better implemented by using a reflex instead of a variable automatic update.

```
species bug {
        ...
	reflex grow {
		float transfer <- min([my_place.food,maxConsumption]);
		size <- size + transfer;
		my_place.food <- my_place.food - transfer;
	}
}
```

### Nota Bene
As you can see the executioner of this reflex is a bug but we could imagine that the cell do the work: it would check if there is an agent within it then transfer food (subtract to its food variable and add to the bug's size variable).
Please check the data-type section for more explanation on this particular type.

<br />

---

## Complete Model

```
model StupidModel3

global torus: true{
	init {
		create bug number: 100 {
			my_place <- one_of(cell);
			location <- my_place.location;
		}
	}
}

grid cell width: 100 height: 100 neighbours: 4 {
	list<cell> neighbours4 <- self neighbours_at 4;
	float maxFoodProdRate <- 0.01;
	float foodProd <- (rnd(1000) / 1000) * maxFoodProdRate;
	float food <- 0.0 update: food + foodProd;
}

species bug {
	cell my_place;
	float size <- 1.0;
	float maxConsumption <- 0.1;
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
	output {
		display stupid_display {
			grid cell;
			species bug aspect: basic;
		}
	}
}

```