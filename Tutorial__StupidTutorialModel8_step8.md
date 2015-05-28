# 8. File output
In the present model, we will show how to write execution information of the simulation to a file for later analysis. To do so, we will also introduce how to work with list.








## Formulation
  * Each time step, write the minimum, mean, and maximum bug size on one line of an output file.





## Model Definition
### writing files
GAMA provides several ways to write files.

A first ways consist in using the statement **file** in the output section: at each simulation step, the expression given is written in the given file.
```
   file file_name type: file_type data: data_to_write;  
```

With:
  * file\_name: string
  * file\_type: string

There are 2 possible types :
  * ‘txt’ (text) : in that case, my\_data is treated as a string, which is written directly in the file
  * ‘csv’ : in that case, my\_data is treated as a list of variables to write : ["var1", "var2", "var3"].

A second way to write files consists in using the save statement:
```
   save my_data type: file_type to: file_name;  
```
With:
  * file\_type : string
  * file\_name : string

There are 3 possible types :
  * ‘txt’ (text) : in that case, my\_data is treated as a string, which is written directly in the file
  * ‘csv’ : in that case, my\_data is treated as a list of values : [val1, val2, val3].
  * ‘shp’ (shapefile - GIS data) : in that case, my\_data is treated as a list of agents : all their geometries are saved in the file (with some variables as attributes). You may refer to [Road traffic tutorial](Tutorial__RoadTrafficTutorial) for more information about shapefiles.

We use this statement (in a global, or world, reflex called **save\_result**) to write:
  * The cycle step: use of the **cycle** keyword that returns the current simulation step.
  * The min and max size of the bug agents: use of **min\_of** and **max\_of** operators which takes a list as left operand and expression as right operand (e.g. **bug min\_of each.size** which search for the minimum size within the bug population).
  * The mean size of the bug agents: use of **list collect expression** to build the list of sizes from the the list of bugs, then **mean(list)** to compute the mean.
```
global torus: true{
       ...
       reflex write_results {
		save [cycle,bug min_of each.size, mean (bug collect each.size),bug max_of each.size] type: "csv" to: "result.csv";
       }
       ...
}
```

Once the simulation is executed you will find the file _result.csv_ located in _model\_directory/models/results.csv_ (you may need to hit `refresh`to see it in the `Gama projects` tab).




## Complete Model

```
model StupidModel8
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
	float food <- 0.0 update: food + foodProd;
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