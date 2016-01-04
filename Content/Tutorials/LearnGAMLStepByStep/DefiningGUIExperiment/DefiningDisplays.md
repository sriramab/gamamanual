# Defining displays

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

Other facets are available when defining your display:
* Use `background` to define a color for your background
```
display "my_display" background:#red
```
* Use `refresh` if you want to refresh the display when a condition is true (to refresh your display every number of steps, use the operator `every`)
```
display "my_display" refresh:every(10)
```

You can choose between two types of displays, by using the facet type:
* java2D displays will be used when you want to have 2D visualization. It is used for example when you manipulate charts. This is the default value for the facet type. 
* opengl displays allows you to have 3D visualization.

You can save the display on the disk, as a png file, in the folder name_of_model/models/snapshots, by using the facet `autosave`. This facet takes one a boolean as argument (to allow or not to save each frame) or a point (to define the size of your image). By default, the resolution of the output image is 500x500.

```
display my_display autosave:true type:java2D {}
```
is equivalent to :
``` 
display my_display autosave:{500,500} type:java2D {}
```

Each display can be decomposed in one or several layers. Here is a screenshot (from the Toy Model Ant) to better understand those different notions we are about to tackle in this session.

(TODO_IMAGE)

## Index

* [2D Layers](#2d-layers)
* [Chart layers](#chart-layers)
* [3D layers](#3d-layers)

## 2D layers

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

(TOTO_IMAGE)

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

(TODO_IMAGE)

To specify a position and a size for your layer, you can use the `position` and the `size` facets.
The `position` facet is used with a point type, between {0,0} and {1,1}, which corresponds to the position of the upper left corner of your layer in percentage. Then, if you choose the point {0.5,0.5}, the upper left corner of your layer will be in the center of your display. By default, this value is {0,0}.
The `size` facet is used with a point type, between {0,0} and {1,1} also. It corresponds to the size occupied by the layer in percentage. By default, this value is {1,1}.

(TODO_IMAGE)

A lot of other facets are available for the different layers. Please read the documentation about this for more information.

## Chart layers

To visualize result and make analysis about you model, you will certainly have to use charts. You can define 3 types of charts in GAML: histograms, pie, and series. For each type, you will have to determine the data you want to highlight.

### Define a chart

To define a chart, we have to use the `chart` statement. A chart has to be named (with the `name` facet), and the type has to be specified (with the `type` facet). The value of the `type` facet can be `histogram`, `pie`, `series`, `scatter`, `xy`. A chart has to be defined inside a display.

```
experiment my_experiment type: gui {
	output {
		display "my_display" {
			chart "my_chart" type:pie {
			}
		}
	}
}
```

After declaring your chart, you have to define the data you want to display in your chart.

### Data definition

Data can be specified with:
* several data statements to specify each series
* one datalist statement to give a list of series. It can be useful if the number of series is unknown, variable or too high.
 
The `data` statement is used to specify which variable will be displayed. You have to give your data a name (that will be displayed in your chart), the value of the variable you want to follow (using the `value` facet). You can add come optional facets such as `color` to specify the color of your data.

``` 
global
{
	int numberA <- 2 update:numberA*2;
	int numberB <- 10000 update:numberB-1000;
}

experiment my_experiment type: gui {
	output {
		display "my_display" {
			chart "my_chart" type:pie {
				data "numberA" value:numberA color:#red;
				data "numberB" value:numberB color:#blue;
			}
		}
	}
}
```

(TODO_IMAGE)

The `datalist` statement is used several variables in one statement.  Instead of giving simple values, datalist is used with lists. 

```
datalist ["numberA","numberB"] value:[numberA,numberB] color:[#red,#blue];
```
[TODO]
Datalist provides you some additional facets you can use. If you want to learn more about them, please read the documentation [URL]

### The different types of chart

As we already said, you can display 3 types of graphs: the histograms, the pies and the series.

The histograms

Quadtree ?
[TODO]


[TODO]

3D Displays

[TODO]
