# Road Traffic



This tutorial has for goal to present the use of GIS data and complex geometries. In particular, this tutorial shows how to load gis data, to agentify them and to use a network of polylines to constraint the movement of agents. All the files related to this tutorial (shapefiles and models) are available in the Models Library (project road\_traffic\_tutorial).

If you are not familiar with agent-based models or GAMA we advice you to have a look at the [prey-predator](https://github.com/mazarsju/gama_doc_17/wiki/Tutorials/Tutorials/PredatorPrey.md) model first.






## Model Overview
The model built in this tutorial concerns the study of the road traffic in a small city. Two layers of GIS data are used: a road layer (polylines) and a building layer (polygons). The building GIS data contain an attribute: the 'NATURE' of each building: a building can be either 'Residential' or 'Industrial'. In this model, people agents are moving along the road network. Each morning, they are going to an industrial building to work, and each night they are coming back home. Each time a people agent takes a road, it wears it out. More a road is worn out, more a people agent takes time to go all over it. The town council is able to repair some roads.

![images/road_traffic.png](images/road_traffic.png)





## Step List

This tutorial is composed of 7 steps corresponding to 7 models. For each step we present its purpose, an explicit formulation and the corresponding GAML code.

  1. [Loading of GIS data (buildings and roads)](https://github.com/mazarsju/gama_doc_17/wiki/Tutorials/Tutorials/RoadTrafficModel/RoadTraficModel_step1.md)
  1. [Definition of people agents](https://github.com/mazarsju/gama_doc_17/wiki/Tutorials/Tutorials/RoadTrafficModel/RoadTraficModel_step2.md)
  1. [Movement of the people agents](https://github.com/mazarsju/gama_doc_17/wiki/Tutorials/Tutorials/RoadTrafficModel/RoadTraficModel_step3.md)
  1. [Definition of weight for the road network](https://github.com/mazarsju/gama_doc_17/wiki/Tutorials/Tutorials/RoadTrafficModel/RoadTraficModel_step4.md)
  1. [Dynamic update of the road network](https://github.com/mazarsju/gama_doc_17/wiki/Tutorials/Tutorials/RoadTrafficModel/RoadTraficModel_step5.md)
  1. [Definition of a chart display](https://github.com/mazarsju/gama_doc_17/wiki/Tutorials/Tutorials/RoadTrafficModel/RoadTraficModel_step6.md)
  1. [Automatic repair of roads](https://github.com/mazarsju/gama_doc_17/wiki/Tutorials/Tutorials/RoadTrafficModel/RoadTraficModel_step7.md)