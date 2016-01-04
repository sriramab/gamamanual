# Predator Prey



This tutorial presents the structure of a GAMA model as well as the use of a grid topology. In particular, this tutorial shows how to define a basic model, to define "grid agents" which are able to move within the constraints. It also introduce the displays and agents' aspect.


All the files related to this tutorial (images and models) are available in the Models Library (project Tutorials/Predator Prey).
## Content





## Model Overview
In this model, three types of entities are considered: preys, predators and vegetation cells. Preys
eat grass on the vegetation cells and predators eat preys. At each simulation step, grass grows on the vegetation cells. Concerning the predators and preys, at each simulation step, they move (to a neighbor cell), eat, die if they do not have enough energy, and eventually reproduce.

![http://gama-platform.googlecode.com/files/predator_prey.png](http://gama-platform.googlecode.com/files/predator_prey.png)
(TODO change url, ainsi que toutes les url du tuto)




## Step List

This tutorial is composed of 12 incremental steps corresponding to 12 models. For each step we present its purpose, an explicit formulation and the corresponding GAML code of the model.

  1. [Basic model (prey agents)](PredatorPreyStep1)
  1. [Dynamic of the vegetation (grid)](PredatorPreyStep2)
  1. [Behavior of the prey agent](PredatorPreyStep3)
  1. [Use of Inspectors/monitors](PredatorPreyStep4)
  1. [predator agents (parent species)](PredatorPreyStep5)
  1. [Breeding of prey and predator agents](PredatorPreyStep6)
  1. [Agent display (aspect)](PredatorPreyStep7)
  1. [Complex behaviors for the preys and predators](PredatorPreyStep8)
  1. [Adding of a stopping condition](PredatorPreyStep9)
  1. [Definition of charts](PredatorPreyStep10)
  1. [Writing files](PredatorPreyStep11)
  1. [Image loading (raster data)](PredatorPreyStep12)