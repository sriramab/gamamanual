# Graphical model of Prey-Predator
`[WORK IN PROGRESS]`


---

GAMA offers two ways to construct a model : writing it directly in GAML or using the [graphical editor](G__GraphicalEditor.md). In this tutorial, we will show you how to use the latter option by re-using the [prey-predator tutorial](Tutorial__PredatorPreyTutorial.md). Thus, you may refer to it if some details are not clear.

Similarly to the original prey-predator model, this tutorial introduces all the standard elements necessary to define an agent-based model in GAMA : a grid topology, agents moving on it and how to visualise the simulation and the overall dynamic thanks to several displays.

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

This tutorial is composed of 7 incremental steps. For each step we present its purpose, an explicit formulation and the corresponding GAML code of the model.

  1. [Basic model (prey agents)](Tutorial__GraphicModel_step1.md)
  1. [Dynamic of the vegetation (grid)](Tutorial__GraphicModel_step2.md)
  1. [Behavior of the prey agent](Tutorial__GraphicModel_step3.md)
  1. [Use of Inspectors/monitors](Tutorial__GraphicModel_step4.md)
  1. [predator agents (parent species)](Tutorial__GraphicModel_step5.md)
  1. [Breeding of prey and predator agents](Tutorial__GraphicModel_step6.md)
  1. [Agent display (aspect)](Tutorial__GraphicModel_step7.md)