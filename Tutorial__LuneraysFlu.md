# Luneray's flu


This tutorial has for goal to introduce how to build a model with GAMA and to use GIS data and graphs. In particular, this tutorial shows how to write a simple GAMA model (the structure of a model, the notion of species...) load gis data, to agentify them and to use a network of polylines to constraint the movement of agents. All the files related to this tutorial (shapefiles and models) are available [here](https://sites.google.com/site/gamatutotp/files/Lunerays%20flu.zip?attredirects=0&d=1).

The importation of models is described here: https://github.com/gama-platform/gama/wiki/G__ImportingModels


## Model Overview
The model built in this tutorial concerns the spreading of a flu in a small city. Two layers of GIS data are used: a road layer (polylines) and a building layer (polygons). In this model, people agents are moving from building to building using the road network. Each infected people can infect the neighbor people.

![http://gama-platform.googlecode.com/files/road_traffic.png](http://gama-platform.googlecode.com/files/road_traffic.png)





## Step List

This tutorial is composed of 5 steps corresponding to 5 models. For each step we present its purpose, an explicit formulation and the corresponding GAML code.

  1. [Creation of a first basic disease spreading model](Tutorial__RoadTraficModel_step1)
  1. [Definition of monitors and chart outputs](Tutorial__RoadTraficModel_step2)
  1. [Importation of GIS data](Tutorial__RoadTraficModel_step3)
  1. [Use of a graph to constraint the movements of people](Tutorial__RoadTraficModel_step4)
  1. [Definition of 3D displays](Tutorial__RoadTraficModel_step5)