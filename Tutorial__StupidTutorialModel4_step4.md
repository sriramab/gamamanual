# 4. Cell and Bug probes
In order to be able to investigate the state of the agent and habitat, we will make the model objects "probeable" from the display.







## Formulation
  * Make the bugs, and the cells, so they can be probed via mouse clicks on the display.




## Model Definition
In GAMA, all agents are automatically probable through inspectors.
Inspectors allow to obtain informations about a species or an agent. There are two kinds of agent information features:
  * Species browser: provides informations about all the agents of a species. Available in the Agents menu ("Population of bug" > "Browse bug population").

![http://gama-platform.googlecode.com/files/browser_table.png](http://gama-platform.googlecode.com/files/browser_table.png)


  * Agent inspector: provides information about one specific agent. It also allows to change the values of its variables during the simulation. Available from the Agents menu, by right\_clicking on a display, in the species inspector or when inspecting another agent. It provides also the possibility to «highlight» the inspected agent.

![http://gama-platform.googlecode.com/files/inspector.png](http://gama-platform.googlecode.com/files/inspector.png)

Note that GAMA interface is "tab-based". You can re-arrange them as you please.





## Complete Model

```
model StupidModel4
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
	float food <- 0.0 update: food + foodProd ;
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