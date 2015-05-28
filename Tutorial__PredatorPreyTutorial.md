# Predator Prey

---

This tutorial presents the structure of a GAMA model as well as the use of a grid topology. In particular, this tutorial shows how to define a basic model, to define "grid agents" which are able to move within the constraints. It also introduce the displays and agents' aspect.


All the files related to this tutorial (images and models) are available in the Models Library (project Tutorials/Predator Prey).
## Content

<br />

---

## Model Overview
In this model, three types of entities are considered: preys, predators and vegetation cells. Preys
eat grass on the vegetation cells and predators eat preys. At each simulation step, grass grows on the vegetation cells. Concerning the predators and preys, at each simulation step, they move (to a neighbor cell), eat, die if they do not have enough energy, and eventually reproduce.

![http://gama-platform.googlecode.com/files/predator_prey.png](http://gama-platform.googlecode.com/files/predator_prey.png)

<br />

---

## Step List

This tutorial is composed of 12 incremental steps corresponding to 12 models. For each step we present its purpose, an explicit formulation and the corresponding GAML code of the model.

  1. [Basic model (prey agents)](Tutorial__PredatorPreyTutorial_step1)
  1. [Dynamic of the vegetation (grid)](Tutorial__PredatorPreyTutorial_step2)
  1. [Behavior of the prey agent](Tutorial__PredatorPreyTutorial_step3)
  1. [Use of Inspectors/monitors](Tutorial__PredatorPreyTutorial_step4)
  1. [predator agents (parent species)](Tutorial__PredatorPreyTutorial_step5)
  1. [Breeding of prey and predator agents](Tutorial__PredatorPreyTutorial_step6)
  1. [Agent display (aspect)](Tutorial__PredatorPreyTutorial_step7)
  1. [Complex behaviors for the preys and predators](Tutorial__PredatorPreyTutorial_step8)
  1. [Adding of a stopping condition](Tutorial__PredatorPreyTutorial_step9)
  1. [Definition of charts](Tutorial__PredatorPreyTutorial_step10)
  1. [Writing files](Tutorial__PredatorPreyTutorial_step11)
  1. [Image loading (raster data)](Tutorial__PredatorPreyTutorial_step12)