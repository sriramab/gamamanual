# 2. Bug Growth
In this step we add a "growth" behavior to our bug agents, it allows us to present the agents' instance variables and methods.


<br />

---


## Formulation
  * Add a second bug action: `grow`. Each time step, a bug grows by a fixed amount (0.1). So bugs need an instance variable for their size, which is initialized to 1.0. This action is scheduled after the `move` action.
  * The bug color on the display is shaded to reflect their size. Bug colors shade from white when `size` is zero to red when `size` is 10 or greater.
<br />

---

## Model Definition

### growing behavior
There is two way to implement the growing behavior: use a reflex or a dynamic variable.

Similarly to the first reflex we defined, you can create a reflex that will increase a `size` variable by 0.1 (used after in the **`aspect`** section).

```
species bug {
	cell my_place;
	float size <- 1.0;
	...
	reflex grow {
		 size <- size + 0.1;
	}
	...
}

```
Another solution is to define an automatic variable update, for example:

```
species bug {
	cell my_place;
	float size <- 1.0 update: size + 0.1;
	...
}

```

Indeed the variable facet **`update`** is evaluated at each time step.
The use of the _automatic update_ is convenient when the bugs growth only depend on parameters. As soon as more complicated process are needed, the implementation based on a reflex is more suitable.

### shading color
We saw previously that we can use **#** + color name to define a color value.

```
rgb color <- #red;
```

Unfortunately it is still uneasy to scale smoothly the color from white to red. Fortunately, it is possible to define one by one the three RGB components of the color using a list of three elements (the red, green and blue components). In our case, we would do as follow:

```
species bug {
	...
	aspect basic {
		int val <- int(255 * (1 - min([1.0,size/10.0])));
		draw circle(size) color: rgb(255,val,val);
	}
}
```

### Nota bene
  * As you can see, it is possible to declare a list by using the brackets and the comma as separator: [elt\_1, elt\_2, elt\_3, etc...]. Here, we have list of two float numbers _[1.0, size/10.0] ._


<br />

---

## Complete Model

```
model StupidModel2

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
}

species bug {
	cell my_place;
	float size <- 1.0;
	reflex basic_move {
		cell destination <- shuffle(my_place.neighbours4) first_with empty(each.agents);
		if (destination != nil) {
			my_place <- destination;
			location <- destination.location;
		}
	}
	reflex grow {
		 size <- size + 0.1;
	}
	aspect basic {
		int val <- int(255 * (1 - min([1.0,size/10.0])));
		draw circle(0.5) color: rgb(255,val,val);
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