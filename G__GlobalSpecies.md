# Global Species (Under Construction)
<font color='red'><i>todo</i>:<br>
<ul><li>move all the attributes to the 'model'/'experiment' species descriptions<br>
</li><li>move all the actions to the 'model' species descriptions<br>
</li><li>proofread the language (sometimes terrible to read !)<br>
</font>
<hr />
The global species defines the attributes, actions and behaviors that describe the world agent. There is one unique world agent per simulation: it is this agent that is created when a user run an experiment and that initializes the simulation through its <b>init</b> section.<br>
The global species is a species like other and can be be manipulated as them. In addition, the global species automatically inherits from several of built-in variables and actions. Note that a specificity of the global species is that all its attributes can be referred by all agents of the simulation.</li></ul>







## Declaration
A GAMA model contains an unique **global** section that defines the global species.

```
global {
}
```

Like for other species, user can define several element inside the global section:

```
species a_name {
   [attribute declarations]
   [init]
   [action declarations]
   [behaviors]
   [aspects]
}
```

In the same way, user can through facets attach skills, a control architecture, define scheduling rules like for other species. See [this page](G__DefiningSpecies) for more details.

A facet that is specific to the global species is the **torus: true/false** one that defines the toroidal properties of the environment.  By default (if this facet is not used) the environment is not torus.

Example:
```
global torus: true {
}
```

Here an example of a global section:
```
global {
	float number_of_bugs <- 1000;
        init {
		create bug number: number_of_bugs ;
	}
}
```

In this case, the world agent will have only one attribute and will, when the user will run an experiment, create **number\_of\_bugs** bug agents.





## Environment Size

The attribute `shape` of the global species allows to define the global environment. GAMA supports three types of topologies for environments: continuous, grid and graph. By default, the world agent has a continuous topology and its geometry is a rectangle of size 100mx100m. The geometry of the environment can be defined:
  * using a geometry: `geometry shape <- rectangle(300,100);`
  * using a shapefile or an OSM file (GIS): envelope of all the data contained in the GIS file: `geometry shape <- envelope("bounds.shp");`,
  * sing a raster file (asc): `geometry shape <- envelope("bounds.asc");`,

Example:

```
global {
	geometry shape <- circle(50);
}
```

```
global {
	file road_shapefile <- file("../includes/roads.shp");
	geometry shape <- envelope(road_shapefile);
}
```

```
global {
	file mnt_file <- file("../includes/mnt.asc");
	geometry shape <- envelope(mnt_file);
}
```





## Built-in Attributes

Like the other attributes of the global species, global built-in attributes can be accessed (and sometimes modified) by the world agent and every other agents in the model.

### world
  * represents the sole instance of the model species (i.e. the one defined in the `global` section). It is accessible from everywhere (including experiments) and gives access to built-in or user-defined global attributes and actions.

### cycle
  * integer, read-only, designates the (integer) number of executions of the simulation cycles. Note that the first cycle is the cycle with number 0.


### step
  * float,  is the length, in model time, of an interval between two cycles, in seconds. Its default value is 1 (second). Each turn, the value of time is incremented by the value of step. The definition of step must be coherent with that of the agents' variables like speed. The use of time unit is particularly relevant for its definition.

```
global {
...
    float step <- 10°h;
...
}
```

### time
  * float, read-only, represents the current simulated time in seconds (the default unit). It is time in the model time. Begins at zero. Basically, we have:   **time = cycle `*` step**  .

```
global {
...
    int nb_minutes function: { int(time / 60)};
...
}
```

### duration
  * string, read-only, represents the value that is equal to the duration **in real machine time** of the last cycle.

### total\_duration
  * string, read-only, represents the sum of duration since the beginning of the simulation.

### average\_duration
  * string, read-only, represents the average of duration since the beginning of the simulation.

### machine\_time
  * float, read-only, represents the current machine time in milliseconds.

### agents
  * list, read-only, returns a list of all the agents of the model that are considered as "active" (i.e. all the agents with behaviors, excluding the places). Note that obtaining this list can be quite time consuming, as the world has to go through all the species and get their agents before assembling the result. For instance, instead of writing something like:

```
ask agents of_species my_species {
...
}
```

one would prefer to write (which is much faster):

```
ask my_species {
...
}
```
Note that any agent has the `agents` attribute, representing the agents it contains. So to get all the agents of the simulation, we need to access the `agents` of the world using: `world.agents`.





## Built-in Actions
The global species is provided with two specific actions.

### halt
  * stops the simulation.

```
global {
     ...
     reflex halting when: empty (agents) {
            do halt;
     }
}
```

### pause
  * pauses the simulation, which can then be continued by the user.

```
global {
     ...
     reflex toto when: time = 100 {
            do pause;
     }
}
```





## Scheduling
In terms of scheduling the world agent is activated first at each time step. It means that the world first acts (update of its attributes, execution of its reflexes), then the agents of the other species act (in random order by default).
It is the same for the init section: first the init section of the world agent is executed, then if agents are created during this execution, the init section of these agents are executed.