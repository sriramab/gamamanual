# Defining Other Layers

---



<br />

---


## agents layer

`agents` allows the modeler to display only the agents that fulfill a given condition.
```
display display_name {
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

For instance, in a segregation model, `agents` will only display happy agents:
```
display Segregation {
   agents agentDisappear value : people as list where (each.is_happy = false) aspect: with_group_color;
}
```
<br />

---


## species layer

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
<br />

---


## image layer
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

<br />

---


## text layer
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
<br />

---

## graphics layer
`graphics` allows the modeler to freely draw shapes/geometries/texts without having to define a species.
The general syntax is:
```
display my_display {
  graphics "my new layer" {
    draw circle(5) at: {10,10} color: rgb("red");
    draw "test" at: {10,10} size: 20 color: rgb("black");
  }
```