# 15. Initialization from a File
Until now we used an environment of fixed size and for which each cell's food production was randomly computed during initialization. In the present model we will see how to use a file to build the environment from.

You may also want to refer to [step 2](Tutorial__PredatorPreyTutorial_step2) of the prey-predator tutorial to have a more detailed presentation of a similar environment construction.


<br />

---


## Formulation
  * Instead of assuming the space size and assuming cell food production is random (model 3), food production rates are read in from a file. The file also determines the space size.
  * The file contains one line per cell, with (a) X coordinate, (b) Y coordinate, and (c) food production rate.
  * Food production in a cell is now equal to the production rate read in from the file, and is no longer random.
  * Now, as we are representing realistic habitat with realistica data (it could be data obtained from satellite photography of land type), it no longer makes sense for the space to be toroidal. So the space objects and movement-related methods must be modified so bugs cannot move off the edge of their space.
  * The input file is `Stupid_Cell.Data` (the file is available in the model library under _Tutorials/Stupid model/data_). It has X, Y, and food production data for a grid space. X ranges from 0 to 250; Y ranges from 0 to 112. The file starts with three lines of header information that is ignored by the model.
  * The cells are now displayed and colored to indicate their current food availability. Cell colors scale from black when cell food availability is zero to green when food availability is 0.5 or higher.
  * A change to the bug move method is required to avoid a very strong artifact now that cell food production is no longer random. Near the start of a simulation, many cells will have exactly the same food availability, so a bug simply would move to the first cell on its list of neighbor cells. This is always the top-left cell among the neighbors, so bugs move constantly up and left if all the cells available to them have the same food availability. This artifact is removed by randomly shuffling the list of available cells before the bug loops through it to identify the best.


<br />

---

## Model Definition
### reading data from a file
GAMA allows to directly read CSV or txt files and to represent them as a matrix using casting operators:

```
global {
    ...
    matrix<float> init_data <- matrix<float>(csv_file("../data/Stupid_Cell.Data", "\t"));
    ...
}
```

In this model, we have to find the X max (width) and the Y max (height). A way to find them is to use the **`max`** operators:

```
global {
    ...
    int width <- int(max (copy_between(init_data column_at 0,3, init_data.rows - 1)));
    int height  <- int(max(copy_between(init_data column_at 1, 3,init_data.rows - 1)));
    geometry shape <- rectangle(width,height);
}
```

Remarks that we use the operator **`copy_between`** to skip the first three lines of header information. Note that in order to keep a cell with a size of 1meter x 1 meter, we redefined the geometry of the world.

In order to set the `foodProd` attribute of each cell, we just have to loop over the matrix rows (from the fourth row), and set the `foodProd` attribute of the right cell using an **`ask`** command.

```
global {
    ...
    init {
        ...
        loop i from: 3 to: ((init_data.rows)) - 1 {
		int ind_i <- int(init_data[0,i]); 
		int ind_j <- int(init_data[1,i]);
		ask cell [ind_i,ind_j] {
			foodProd <- init_data[2,i];
		}  
	} 
    }
    ...
}
```

### cell color
In a similar way than for the bugs (model 2), we have to dynamically compute the color of the cell according to the food availability.

```
grid cell width: width height: height neighbours: 4 {
	...
	rgb color <- rgb(0, min([255, int(food * 255 *2)]), 0) update: rgb(0,min([255, int(food * 255 * 2)]), 0);
}
```

We used the **`min`** operator to ensure that the value for the green will be lower or equal to 255.

### modification of the bug behaviour
We have to modify the bug behaviour by randomly shuffling the list of available cells before the bug loops through it to identify the best. The shuffling of a list is very simple in GAMA using the `shuffle` operator.

```
species bug schedules: bug sort_by ( - each.size){
	...
	reflex basic_move {
		cell destination <- shuffle(my_place.neighbours4 where empty(each.agents) + my_place) with_max_of (each.food);
		if (destination != nil) {
			my_place <- destination;
			location <- destination.location;
		}
	}
```


<br />

---

## Complete Model

```
model StupidModel15

global {
    int numberBugs <- 100;
    float globalMaxConsumption <- 1.0;
    float globalMaxFoodProdRate <- 0.01;
    float initialBugSizeMean <- 0.1;
    float initialBugSizeSD <- 0.03;
    matrix<float> init_data <- matrix<float>(csv_file("../data/Stupid_Cell.Data", "\t"));
    int width <- int(max (copy_between(init_data column_at 0,3, init_data.rows - 1)));
    int height  <- int(max(copy_between(init_data column_at 1, 3,init_data.rows - 1)));
    geometry shape <- rectangle(width,height);
    init {
		create bug number: numberBugs {
			my_place <- one_of(cell);
			location <- my_place.location;
		}
		loop i from: 3 to: ((init_data.rows)) - 1 {
			int ind_i <- int(init_data[0,i]); 
			int ind_j <- int(init_data[1,i]);
			ask cell [ind_i,ind_j] {
				foodProd <- init_data[2,i];
			}  
		} 
     }
     reflex shouldHalt when: cycle = 999 or empty(bug)  {
		 do halt;
     }
     reflex write_results {
		save [cycle,bug min_of each.size, mean (bug collect each.size),bug max_of each.size] type: "csv" to: "result.csv"; 
     }
	
}

grid cell width: width height: height neighbours: 4 {
	list<cell> neighbours4 <- self neighbours_at 4;
	list<cell> neighbours3 <- self neighbours_at 3;
	float maxFoodProdRate <- globalMaxFoodProdRate;
	float foodProd <- (rnd(1000) / 1000) * maxFoodProdRate;
	float food <- 0.0 update: food + foodProd;
	rgb color <- rgb(0, min([255, int(food * 255 *2)]), 0) update: rgb(0,min([255, int(food * 255 * 2)]), 0);
}

species bug schedules: bug sort_by ( - each.size){
	cell my_place;
	float size <- max([0,gauss(initialBugSizeMean,initialBugSizeSD)]);
	float maxConsumption <- globalMaxConsumption;
	float survivalProbability <- 0.95;
	reflex basic_move {
		cell destination <- shuffle(my_place.neighbours4 where empty(each.agents) + my_place) with_max_of (each.food);
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