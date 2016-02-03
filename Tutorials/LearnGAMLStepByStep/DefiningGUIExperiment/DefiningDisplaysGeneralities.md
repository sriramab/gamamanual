[//]: # (startConcept|2d_layers)
# Defining displays (Generalities)
[//]: # (keyword|concept_displays)
[//]: # (keyword|concept_layers)
[//]: # (keyword|concept_output)

## Index

* [Displays and layers](#displays-and-layers)
* [Organize your layers](#organize-your-layers)
* [Example of layers](#example-of-layers)
  * [agents layer](#agents-layer)
  * [species layer](#species-layer)
  * [image layer](#image-layer)
  * [text layer](#text-layer)
  * [graphics layer](#graphics-layer)

## Displays and layers

A display is the graphical output of your simulation. You can define several displays related with what you want to represent from your model execution. To define a display, use the keyword `display` inside the `output` scope, and specify a name (`name` facet).

```
experiment my_experiment type: gui {
	output {
		display "display1" {
		}
		display name:"display2" {
		}
	}
}
```

[//]: # (keyword|concept_background)
Other facets are available when defining your display:
* Use `background` to define a color for your background
```
display "my_display" background:#red
```
[//]: # (keyword|concept_refresh)
* Use `refresh` if you want to refresh the display when a condition is true (to refresh your display every number of steps, use the operator `every`)
```
display "my_display" refresh:every(10)
```

You can choose between two types of displays, by using the facet type:
* java2D displays will be used when you want to have 2D visualization. It is used for example when you manipulate charts. This is the default value for the facet type. 
* opengl displays allows you to have 3D visualization.

[//]: # (keyword|concept_autosave)
You can save the display on the disk, as a png file, in the folder name_of_model/models/snapshots, by using the facet `autosave`. This facet takes one a boolean as argument (to allow or not to save each frame) or a point (to define the size of your image). By default, the resolution of the output image is 500x500.

```
display my_display autosave:true type:java2D {}
```

is equivalent to :

``` 
display my_display autosave:{500,500} type:java2D {}
```

Each display can be decomposed in one or several layers. Here is a screenshot (from the Toy Model Ant) to better understand those different notions we are about to tackle in this session.

![images/difference_layer_display.png](resources/images/definingGUIExperiment/difference_layer_display.png)

## Organize your layers

In one 2D display, you will have several types of layers, giving what you want to display in your model. Each layer will be displayed in the same order as you declare them. The last declared layer will be above the others.

Thus, the following code:

```
experiment expe type:gui {
	output {
		display my_display {
			graphics "layer1" {
				draw square(20) at:{10,10} color:#red;
			}
			graphics "layer2" {
				draw square(20) at:{15,15} color:#blue;
			}
			graphics "layer3" {
				draw square(20) at:{20,20} color:#yellow;
			}
		}
	}
}
```

Will have this output:

![images/layers_order.png](resources/images/definingGUIExperiment/layers_order.png)

You have a large number of layers available. You already know some of them, such as `species`, `agents`, `grid`, but other specific layers such as `image` (to display image), `text` (to display text) and `graphics` (to freely draw shapes/geometries/texts without having to define a species) are also available:

```
experiment expe type:gui {
	output {
		display display_an_image {
		   image "layer_name" file:"../images/my_image.png";
		}
		display display_a_text {
		   text "layer_name" value:"here your text";
		}
		display display_some_geometry {
			graphics "my_layer" {
				draw rectangle(2,5);
				draw text:"here a text";
			}
		}
	}
}
```

[//]: # (keyword|concept_transparency)
Most of the layers have the `transparency` facet in order to see the layers which are under.

```
experiment expe type:gui {
	output {
		display my_display {
			graphics "layer1" {
				draw square(20) at:{10,10} color:#red;
			}
			graphics "layer2" transparency:0.5 {
				draw square(20) at:{15,15} color:#blue;
			}
		}
	}
}
```

![images/layers_transparency.png](resources/images/definingGUIExperiment/layers_transparency.png)

To specify a position and a size for your layer, you can use the `position` and the `size` facets.
The `position` facet is used with a point type, between {0,0} and {1,1}, which corresponds to the position of the upper left corner of your layer in percentage. Then, if you choose the point {0.5,0.5}, the upper left corner of your layer will be in the center of your display. By default, this value is {0,0}.
The `size` facet is used with a point type, between {0,0} and {1,1} also. It corresponds to the size occupied by the layer in percentage. By default, this value is {1,1}.

![images/layers_size_position.png](resources/images/definingGUIExperiment/layers_size_position.png)

A lot of other facets are available for the different layers. Please read the documentation about this for more information.

## Example of layers

### agents layer
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
  image background file:"../images/my_backgound.jpg";
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
`graphics` allows the modeler to freely draw shapes/geometries/texts without having to define a species.
The general syntax is:
```
display my_display {
  graphics "my new layer" {
    draw circle(5) at: {10,10} color: rgb("red");
    draw "test" at: {10,10} size: 20 color: rgb("black");
  }
```
[//]: # (endConcept|2d_layers)