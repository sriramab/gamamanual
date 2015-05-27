

# <font color='blue'>Definition of GUI experiment</font>

A GUI experiment allows to display a graphical interface with input parameters and outputs (display, file, monitor...).

A GUI experiment is defined by:

```
experiment exp_name type: gui {
   [input]
   [output]
}
```

# <font color='blue'>Input</font>

## Parameters
Experiments can define input, i.e. parameters.
Defining parameters allows to make the value of a global variable definable by the user through the user graphic interface.

A parameter is defined as follow:

```
   parameter title var: global_var category: cat;
```

With:
  * title: string to display
  * var: reference to a global variable (defined in the global section)
  * category: string used to «store» the operators on the UI (optional)

Example:
```
   parameter "Value of toto: " var: toto;
```

## User command

Experiments can also define some commands (buttons in the GUI) allowing the user to interact with the simulation, i.e. to call an action defined in the model. Commands can either call directly an existing action (with or without arguments) or be followed by a block that describes what to do when this command is run. The syntax is:
```
   user_command cmd_name action: action_name;
```
or
```
   user_command cmd_name action: action_name with: [arg1::val1, arg2::val2, ...];
```
or
```
   user_command cmd_name {
	[statements]
   }
```

These commands are not executed when an agent runs. Instead, they are collected and appear as buttons above the parameters of the simulation.


# <font color='blue'>Output</font>

Output blocks define how to visualize a simulation (with one or more display blocks that define separate windows)
```
experiment exp_name type: gui {
   [input]
   output {
     [display statements]
     [monitor statements]
     [file statements]
   }
}
```

## Display

A display refers to a independent and mobile part of the interface that can display species, images, texts or charts.

The general syntax is:
```
display my_display [additional options] { ... }
```

Additional options include:
  * **`background`** (type = color): the color of the display background
  * **`type`** (2 possible values: java2D or opengl): specify if the display will use the java 2D ou openGL libraries. Note that the openGl display does not admit charts. The default value is java2D.
  * **`refresh_every`** (type = int): the display will be refreshed every nb steps of the simulation
  * **`autosave`** (type = boolean or location): if the value is true or is a location, GAMA will take each a snapshot of the display every time the display is refreshed. The location will precise the dimaension of the picture.


There exist several kinds of display:
  * classical **displays** (without specific type) used to species, text, image, charts...
```
display my_display { ... }
```
  * **opengl displays** (display with `type: opengl`) used to display species, text or image. It allows to display 3D models.
```
display my_display type: opengl { ... }
```
  * **graphdisplay** is a special kind of display dedicated to the display of graphs. It is based on the graphstream library. Note that it provides a pretty way of displaying graphs without regard of spatiality.
```
graphdisplay monNom2 graph: my_graph lowquality:true ;
```

Each display can be refreshed independently by defining the facet **refresh\_every: nb (int)** (the display will be refreshed every nb steps of the simulation)

Each display can include different layers (like in a GIS). Although every combinaison of any number of following layers are allowed in GAML, it is recommended to distinguish displays with species, image and/or text and display with charts (and text).


### agents layer

`agents` allows the modeler to display only the agents that fulfill a given condition.
```
display my_display {
   agents layer_name value: expression [additional options];
}
```
Additional options include:
  * **`value`** (type = container) the set of agents to display
  * **`aspect`**: the name of the aspect that should be used to display the species.
  * **`transparency`** (type = float, from 0 to 1): the transparency rate of the agents (1 means no transparancy)
  * **`position`** (type = point, from {1,1} to {0,0}): position of the upper-left corner of the layer (note that {0.5,0.5} refers to the middle of the display)
  * **`size`** (type = point, from {1,1} to {0,0}): size of the layer ({1,1} refers to the original size whereas {0.5,0.5} divides by 2 the height and the width of the layer)
  * **`refresh`** (type = boolean, **opengl only**): specify whether the display of the species is refreshed. (usefull in case of agents that do not move)
  * **`z`** (type = float, from 0 to 1, **opengl only**): altitude of the layer displaying agents
  * **`focus`** (type = agent)

For instance, in a segregation model, `agents` will only display un happy agents:
```
display Segregation {
   agents agentDisappear value : people as list where (each.is_happy = false) aspect: with_group_color;
}
```


### species layer

`species` allows modeler to display all the agent of a given species in the current display. In particular, modeler can choose the aspect used to display them.

The general syntax is:
```
display display_name {
   species species_name [additional options];
}
```
Additional options include:
  * **`aspect`**: the name of the aspect that should be used to display the species.
  * **`transparency`** (type = float, from 0 to 1): the transparency rate of the agents (1 means no transparancy)
  * **`position`** (type = point, from {1,1} to {0,0}): position of the upper-left corner of the layer (note that {0.5,0.5} refers to the middle of the display)
  * **`size`** (type = point, from {1,1} to {0,0}): size of the layer ({1,1} refers to the original size whereas {0.5,0.5} divides by 2 the height and the width of the layer)
  * **`refresh`** (type = boolean, **opengl only**): specify whether the display of the species is refreshed. (usefull in case of agents that do not move)
  * **`z`** (type = float, from 0 to 1, **opengl only**): altitude of the layer displaying agents

For instance it could be:
```
display my_display{
  species agent1 aspect: base ;
}
```

Species can be superposed on the same plan:
```
display my_display{
  species agent1 aspect: base;
  species agent2 aspect: base;
  species agent3 aspect: base;
}
```

Species can be placed on different z values for each layer using the opengl display. z:0 means the layer will be placed on the ground and z=1 means it will be placed at an height equal to the maximum size of the environment.
```
display my_display type: opengl{
  species agent1 aspect: base z:0;
  species agent2 aspect: base z:0.5;
  species agent3 aspect: base z:1;
}
```


### image layer
`image` allows modeler to display an image (e.g. as background of a simulation).
The general syntax is:
```
display display_name {
   image layer_name file: image_file [additional options];
}
```
Additional options include:
  * **`file`** (type = string): the name/path of the image (in the case of a raster image)
  * **`gis`** (type = string): the name/path of the shape file (to display a shapefile as background, without creating agents from it)
  * **`color`** (type = color): in the case of a shapefile, this the color used to fill in geometries of the shapefile
  * **`transparency`** (type = float, from 0 to 1): the transparency rate (1 means no transparancy)
  * **`position`** (type = point, from {1,1} to {0,0}): position of the upper-left corner of the layer (note that {0.5,0.5} refers to the middle of the display)
  * **`size`** (type = point, from {1,1} to {0,0}): size of the layer ({1,1} refers to the original size whereas {0.5,0.5} divides by 2 the height and the width of the layer)
  * **`refresh`** (type = boolean, **opengl only**): specify whether the display of the image is refreshed.
  * **`z`** (type = float, from 0 to 1, **opengl only**): altitude of the layer displaying the image

For instance:
```
display my_display{
  image background file:"../images/my_backgound.jpg"
}
```
Or
```
display city_display refresh_every: 1 {
   image testGIS gis: "../includes/building.shp" color: rgb('blue');
}
```

It is also possible to superpose images on different layers in the same way as for species using opengl display.
```
display my_display type:opengl{
  image image1 file:"../images/image1.jpg";
  image image2 file:"../images/image2.jpg" z:0.5;
}
```


### chart layer

`chart` allows modeler to display a chart: this enables to display a specific value of the model at each iteration. GAMA can display various chart types: time series (**series**), pie charts (**pie**) and histograms (**histogram**).
```
display chart_display [additional options] {
  chart  "chart name" type: series {
  data data1 value: mydata1 color: rgb('blue') ;
  data data2 value: mydata2 color: rgb('blue') ;
}
```

Additional options include:
  * **`transparency`** (type = float, from 0 to 1): the transparency rate of the layer (1 means no transparancy)
  * **`position`** (type = point, from {1,1} to {0,0}): position of the upper-left corner of the layer (note that {0.5,0.5} refers to the middle of the display)
  * **`size`** (type = point, from {1,1} to {0,0}): size of the layer ({1,1} refers to the original size whereas {0.5,0.5} divides by 2 the height and the width of the layer)
  * **`background`** (type = color): the background color
  * **`axes`** (type = color): the axes color
  * **`type`**: the type of chart. It could be **histogram**, **series**, **xy** or **pie**. The difference between **series** and **xy** is that the former adds an implicit x-axis that refers to the numbers of cycles, while the latter considers the first declaration of **data** to be its x-axis.
  * **`style`**: the style of the chart. It could be: **exploded**, **stack**, **bar** or **3d**
  * **`font`**: the font used for legends.
  * **`color`** (type = color)


### text layer
`text` allows the modeler to display a string (that can change at each step) in a given position of the display.
The general syntax is:
```
display my_display {
  text  my_text value: expression [additional options];
```

Additional options include:
  * **`value`** (type = string) the string to display
  * **`transparency`** (type = float, from 0 to 1): the transparency rate of the layer (1 means no transparancy)
  * **`position`** (type = point, from {1,1} to {0,0}): position of the upper-left corner of the layer (note that {0.5,0.5} refers to the middle of the display)
  * **`size`** (type = point, from {1,1} to {0,0}): size of the layer ({1,1} refers to the original size whereas {0.5,0.5} divides by 2 the height and the width of the layer)
  * **`font`**: the font used for the text
  * **`color`** (type = color): the color used to display the text
  * **`refresh`** (type = boolean, **opengl only**): specify whether the layer is refreshed.
  * **`z`** (type = float, from 0 to 1, **opengl only**): altitude of the layer displaying text

For instance:
```
display my_display {
   text agents value : 'Carrying ants : ' + string ( int ( ant as list count (each . has_food ) ) + int ( ant as list count ( each . state =    'followingRoad' ) ) ) position : { 0.5 , 0.03 } color : rgb ( 'black' ) size: { 1 , 0.02 };  
}
```

### graphics layer
`graphics` allows the modeler to freely draw shapes/geometries/texts without having to define a species. It works exactly like a species [aspect](https://code.google.com/p/gama-platform/wiki/Aspect16): The **draw** statement can be used in the same way.
The general syntax is:
```
display my_display {
  graphics "my new layer" {
    draw circle(5) at: {10,10} color: rgb("red");
    draw "test" at: {10,10} size: 20 color: rgb("black");
  }
```


### event
Allows to interact with the simulation by capturing mouse event and do an action. This action could apply a change on environment or on agents, according to the goal.

Events are determine for a display. Thus, they can be play a different behavior

```
event [event_type] action: myAction
```
  * event\_type mouse\_down or mouse\_up
  * myAction is an action written in the global block. This action have to follow the specification below.

```

 global
 {
   ...
   action myAction (point location, list selected_agents)
   {
      // location: contains le location of the click in the environment
      // selected_agents: contains agents clicked by the event
    
    ... //code written by the authors ...
   } 
 }

 experiment Simple type:gui {
	parameter 'Evaporation Rate:' var: evaporation_rate;
	parameter 'Diffusion Rate:' var: diffusion_rate;
	output { 
		display Ants refresh_every: 2 { 
			grid ant_grid;
			species ant aspect: default;
			event mouse_up action: myAction;
		}  

...

```


## Monitor

A monitor allows to follow the value of an arbitrary expression in GAML.
Definition of a monitor:
```
monitor monitor_name value: an_expression refresh_every: nb_steps;
```
with:
  * value: mandatory, its value will be displayed in the monitor.
  * refresh\_every: int, optional : number of simulation steps between two computations of the expression (default is 1).

Example:
```
  monitor "nb preys" value: length(prey as list);  
```