
<br />
# <font color='blue'>Introduction</font>
This tutorial has for goal to present the use of GIS data and complex geometries. In particular, this tutorial shows how to load gis data, to agentify them and to use a network of polylines to constraint the movement of agents. All the files related to this tutorial (shapefiles and models) are available in the Models Library (project road\_traffic\_tutorial).

The model built in this tutorial concerns the study of the road traffic in a small city. Two layers of GIS data are used: a road layer (polylines) and a building layer (polygons). The building GIS data contain an attribute: the 'NATURE' of each building: a building can be either 'Residential' or 'Industrial'. In this model, people agents are moving along the road network. Each morning, they are going to an industrial building to work, and each night they are coming back home. Each time a people agent takes a road, it wears it out. More a road is worn out, more a people agent takes time to go all over it. The town council is able to repair some roads.

![http://gama-platform.googlecode.com/files/road_traffic.png](http://gama-platform.googlecode.com/files/road_traffic.png)


# <font color='blue'>Road traffic in a city: model list</font>

This tutorial is composed of 7 models. For each model we will present its purpose, an explicit formulation and the corresponding GAML code.

  1. [Loading of GIS data (buildings and roads)](RoadTraficModel1v16.md)
  1. [Definition of people agents](RoadTraficModel2v16.md)
  1. [Movement of the people agents](RoadTraficModel3v16.md)
  1. [Definition of weight for the road network](RoadTraficModel4v16.md)
  1. [Dynamic update of the road network](RoadTraficModel5v16.md)
  1. [Definition of a chart display](RoadTraficModel6v16.md)
  1. [Automatic repair of roads](RoadTraficModel7v16.md)