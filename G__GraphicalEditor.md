# The Graphical Editor

---


The graphical editor that allow to build diagram (gadl files) is based on the [Graphiti](http://www.eclipse.org/graphiti/) Eclipse plugin. It allows to define a GAMA model through a graphical interface. It a allows as well to produce a graphical model (diagram) from a gaml model.

![http://gama-platform.googlecode.com/files/gm_predator_prey.png](http://gama-platform.googlecode.com/files/gm_predator_prey.png)



<br />

---

## Installing the graphical editor
Using the graphical editor requires toinstall the graphical modeling plug-in. See [here](G__InstallingPlugins.md) for information about plug-ins and their installation.

The graphical editor plug-in is called **Graphical\_modeling** and is directly available from GAMA update site **https://gama-platform.googlecode.com/svn/update_site/*.**

<br />
<img src='https://gama-platform.googlecode.com/svn/wiki/images/graphical_editor/installing_graphical_editor.JPG' /> <br />
<br />

Note that the graphical editor is still under development. Updates of the plug-in will be add to the GAMA website. After installing the plug-in (and periodically), check for updates for this plug-in: in the "Help" menu, choose "Check for Updates" and install the proposed updates for the graphical modeling plug-in.


---

## Creating a first model

A new diagram can be created in a new GAMA project. First, right click on a project, then select "New" on the contextual menu.
In the New Wizard, select "GAMA -> Model Diagram", then "Next>"
![http://gama-platform.googlecode.com/files/newDiagram.png](http://gama-platform.googlecode.com/files/newDiagram.png)

In the next Wizard dialog, select the type of diagram (Empty, Skeleton or Example) then the name of the file and the author.

<br />![http://gama-platform.googlecode.com/files/modeldiagramNew.png](http://gama-platform.googlecode.com/files/modeldiagramNew.png) <br />

Skeleton and Example diagram types allow to add to the diagram some basic features.

<br />

---

## Status of models in editors

Similarly to GAML editor, the graphical editor proposes a live display of errors and model statuses. A graphical model can actually be in three different states, which are visually accessible above the editing area: **Functional** (orange color), **Experimentable** (green color) and **InError** (red color). See [the section on model compilation](CompilingModels161.md) for more precise information about these statuses.

In its initial state, a model is always in the **Functional** state, which means it compiles without problems, but cannot be used to launch experiments. The **InError** state occurs when the file contains errors (syntactic or semantic ones).

Reaching the **Experimentable** state requires that all errors are eliminated and that at least one experiment is defined in the model. The experiment is immediately displayed as a button in the toolbar, and clicking on it will allow to launch this experiment on your model.

Experiment buttons are updated in real-time to reflect what's in your code. If more than one experiment is defined, corresponding buttons will be displayed in addition to the first one.

<br />

---

## Diagram definition framework

The following figure presents the editing framework:
![http://gama-platform.googlecode.com/files/framework.png](http://gama-platform.googlecode.com/files/framework.png)

<br />

---

## Features

### agents
#### species

![http://gama-platform.googlecode.com/files/species.png](http://gama-platform.googlecode.com/files/species.png)

The species feature allows to define a species with a continuous topology. A species is always a micro-species of another species. The top level (macro-species of all species) is the world species.

  * **source**: a species (macro-species)
  * **target**: -
![http://gama-platform.googlecode.com/files/Frame_Speciesdef1.png](http://gama-platform.googlecode.com/files/Frame_Speciesdef1.png)

![http://gama-platform.googlecode.com/files/Frame_Speciesdef2.png](http://gama-platform.googlecode.com/files/Frame_Speciesdef2.png)

#### grid

![http://gama-platform.googlecode.com/files/grid.png](http://gama-platform.googlecode.com/files/grid.png)

The grid feature allows to define a [species](Species151.md) with a [grid topology](Sections151#environment.md). A grid is always a micro-species of another species.

  * **source**: a species (macro-species)
  * **target**: -

![http://gama-platform.googlecode.com/files/Frame_grid.png](http://gama-platform.googlecode.com/files/Frame_grid.png)

#### Inheriting link
The inheriting link feature allows to define an inheriting link between two species.

  * **source**: a species (parent)
  * **target**: a species (child)

![http://gama-platform.googlecode.com/files/inhereting_link.png](http://gama-platform.googlecode.com/files/inhereting_link.png)


#### world

![http://gama-platform.googlecode.com/files/world.png](http://gama-platform.googlecode.com/files/world.png)

When a model is created, a world species is always defined. It represent the global part of the model. The world species, which is unique, is the top level species. All other species are micro-species of the world species.

![http://gama-platform.googlecode.com/files/Frame_world.png](http://gama-platform.googlecode.com/files/Frame_world.png)

### agent features

#### action
![http://gama-platform.googlecode.com/files/action.png](http://gama-platform.googlecode.com/files/action.png)

The action feature allows to define an action for a species.

  * **source**: a species (owner of the action)
  * **target**: -

![http://gama-platform.googlecode.com/files/Frame_action.png](http://gama-platform.googlecode.com/files/Frame_action.png)

#### reflex
![http://gama-platform.googlecode.com/files/reflex.png](http://gama-platform.googlecode.com/files/reflex.png)

The reflex feature allows to define a reflex for a species.

  * **source**: a species (owner of the reflex)
  * **target**: -

![http://gama-platform.googlecode.com/files/Frame_reflex.png](http://gama-platform.googlecode.com/files/Frame_reflex.png)

#### aspect
![http://gama-platform.googlecode.com/files/aspect.png](http://gama-platform.googlecode.com/files/aspect.png)

The aspect feature allows to define an aspect for a species.

  * **source**: a species (owner of the aspect)
  * **target**: -

![http://gama-platform.googlecode.com/files/Frame_aspect.png](http://gama-platform.googlecode.com/files/Frame_aspect.png)


![http://gama-platform.googlecode.com/files/Frame_Aspect_layer.png](http://gama-platform.googlecode.com/files/Frame_Aspect_layer.png)
### experiment
#### GUI experiment

![http://gama-platform.googlecode.com/files/guiXP.png](http://gama-platform.googlecode.com/files/guiXP.png)

The GUI Experiment feature allows to define a GUI experiment.

  * **source**: world species
  * **target**: -

![http://gama-platform.googlecode.com/files/Frame_Experiment.png](http://gama-platform.googlecode.com/files/Frame_Experiment.png)

#### display

![http://gama-platform.googlecode.com/files/display.png](http://gama-platform.googlecode.com/files/display.png)

The display feature allows to define a display.

  * **source**: GUI experiment
  * **target**: -

![http://gama-platform.googlecode.com/files/Frame_display.png](http://gama-platform.googlecode.com/files/Frame_display.png)


![http://gama-platform.googlecode.com/files/Frame_layer_display.png](http://gama-platform.googlecode.com/files/Frame_layer_display.png)

#### batch experiment

![http://gama-platform.googlecode.com/files/batchxp.png](http://gama-platform.googlecode.com/files/batchxp.png)

The Batch Experiment feature allows to define a Batch experiment.

  * **source**: world species
  * **target**: -

<br />

---

## Pictogram color modification
It is possible to change the color of a pictogram.
  * Right click on a pictogram, then select the "Chance the color".

<br />

---

## GAML Model generation
It is possible to automatically generate a Gaml model from a diagram.
  * Right click on the graphical framework (where the diagram is defined), then select the "Generate Gaml model".
A new GAML model with the same name as the diagram is created (and open).