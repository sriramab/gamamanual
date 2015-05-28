# Chart Layer (Under construction)









```
display chart_display [additional options] {
  chart  "chart name" type: series {
  data data1 value: mydata1 color: rgb('blue') ;
  data data2 value: mydata2 color: rgb('blue') ;
}
```

## Chart type

`chart` allows modeler to display a chart:
GAMA can display 3 main types of charts using the **`type`** facet:

  * histograms (**histogram**)

  * pie (**pie**)

  * series/xy/scatter: both display series with lines or dots, with 3 subtypes :
    * series (**series**) : to display the evolution of one/several variable (vs time or not).
    * xy (**xy**) : to specify both x and y value. To allow stacked plots, only one y value for each x value.
    * scatter (**scatter**) : free x and y values for each serie.

chart options include:
  * **axes** optional, expects a rgb - the axis color
  * **background** optional, expects a rgb - the background color
  * **position** optional, expects a point - position of the upper-left corner of the layer. Note that if coordinates are in [0,1[, the position is relative to the size of the environment (e.g. {0.5,0.5} refers to the middle of the display) whereas it is absolute when coordinates are greter than 1. The position can only be a 3D point {0.5, 0.5, 0.5}, the last coordinate specifying the elevation of the layer.
  * **size** optional, expects a point - the layer resize factor: {1,1} refers to the original size whereas {0.5,0.5} divides by 2 the height and the width of the layer. In case of a 3D layer, a 3D point can be used (note that {1,1} is equivalent to {1,1,0}, so a resize of a layer containing 3D objects with a 2D points will remove the elevation)
  * **style** optional, expects an identifier, takes values in {stack, 3d, bar, exploded}. - No documentation yet
  * **timexseries** optional, expects a list - for series charts, change the default time serie (simulation cycle) for an other value.
  * **transparency** optional, expects a float - the style of the chart
  * **x\_range**, optional, expects any type in [float, a int, a point](a) - range of the x-axis. Can be a number (which will set the axis total range) or a point (which will set the min and max of the axis).
  * **x\_tick\_unit**, optional, expects a float - the tick unit for the y-axis (distance between horyzontal lines and values on the left of the axis).
  * **y\_range**, optional, expects any type in [float, a int, a point](a) - range of the y-axis. Can be a number (which will set the axis total range) or a point (which will set the min and max of the axis).
  * **y\_tick\_unit**, optional, expects a float - the tick unit for the x-axis (distance between vertical lines and values bellow the axis).

## Data definition

Data can be specified with:

  * several **data** statements to specify each serie

  * one **datalist** statement to give a list of series. It can be useful if the number of series is unknown, variable or too high.

### data statement

One data statement is used for one serie.
```
chart "DataBar" type:histogram
{
	data "empty_ants" value:(list(ant) count (!each.hasFood)) color:°red;
	data "carry_food_ants" value:(list(ant) count (each.hasFood)) color:°green;				
}
```

Only the value facet is required to provide the data value. It can be a single value (for histograms/pies/temporal series), lists (for series), points (for xy/scatter) or list of points (for scatter).
Other options include:
  * **color**, expects a rgb
  * **fill**, expects a bool, to specify is the marker is filled or not
  * **line\_visible**, expects a bool, to specify if the line is visible or not (set to false to get a classic scatter plot)
  * **marker**, expects a bool, to specify if the marker is visible or not
  * **marker\_shape**, takes values in {marker\_square, marker\_left\_triangle, marker\_right\_triangle, marker\_diamond, marker\_hor\_rectangle, marker\_hor\_ellipse, marker\_vert\_rectangle, marker\_empty, marker\_up\_triangle, marker\_sqaure, marker\_down\_triangle}.
  * **style**, takes values in {exploded, dot, bar, step, area\_stack, whisker, ring, line, 3d, spline, area, stack}. Available styles depend on the chart style (see bellow for each chart style).

### datalist statement

One datalist statement is used for all the series.
```
chart "DataListBar" type:histogram
{
	datalist ["empty","carry"] value:[(list(ant) count (!each.hasFood)),(list(ant) count (each.hasFood))] color:[°red,°green];				
}
```

Only the value facet is required to provide the data values.
It can be:
  * a list of numbers (for histograms/pies/temporal series)
  * a list of list of numbers (for histograms/series)
  * a list of points/list with two numbers (for temporal xy/scatter)
  * a list of list of points/lists with two numbers (for xy/scatter)

The number of series and values per serie (categories) doesn't have to be fixed, and series/categories names can change at each step.
Series and categories names are set by :
  * **categoriesnames** facet, with a list of string
  * **legend** facet, with a list of string

Since you often have list of lists, it is possible to reverse categories and series using the **inverse\_series\_categories** keyword.
For example inverse\_series\_categories=true will transform a value of [[1,2,3],[4,5,6]] to [[1,4],[2,5],[3,6]]. It May be useful when it is easier to construct one list over the other.

Other options include:

  * **color**, expects a list of colors
  * **fill**, optional, expects a bool - same as data statement
  * **line\_visible**, optional, expects a bool - same as data statement
  * **marker**, optional, expects a bool - same as data statement
  * **style**, optional, expects an identifier, takes values in {exploded, dot, bar, step, area\_stack, whisker, ring, line, 3d, spline, area, stack}. - same as data statement


## Series/xy/scatter charts details

For series/xy/scatter charts
  * With data statement, if each value is a single number, the value will be added to the chart at each chart step. If the value is a list, the value will be replaced by the list at each step.
  * With datalist statement, if each value is a list of numbers, the value will be added to the chart at each chart step. If the value is a list of lists, the value will be replaced by the list at each step.

For example, this chart displays the positions of all the ants at each step (with two series):

```
display ChartScatterList {
	chart "DataListScatter" type:scatter
	{
		datalist ["empty","carry"] value:[((list(ant) where (!each.hasFood))  collect each.location),((list(ant) where (each.hasFood))  collect each.location)] color:[°red,°green] line_visible:false;				
	}
}
```

This one will display the history of the "average" ant with and without food:
```
display ChartScatterHistory {
	chart "DataListScatterHistory" type:scatter
	{
		datalist ["empty","carry"] value:[mean((list(ant) where (!each.hasFood)) collect each.location),mean((list(ant) where (each.hasFood)) collect each.location)]
			 color:[°red,°green] line_visible:true;				
	}
}
```