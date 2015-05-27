
<br />
# <font color='blue'> Introduction </font>

Developed as a plugin of Eclipse, GAMA has an graphical user interface very close to the Eclipse one. It is in particular based on the notions of editor, view and perspective.

**Views** and **editors** and tabs in which user can display information (in the case of view) and edit files (in the case of editors). For example, the _Gama_ _Navigator_ allows to display the projects libraries.

A **Perspective** a visual container in which are organized a set of views and editors.


# <font color='blue'> GAMA perspectives </font>
## List of GAMA perspectives
GAMA provides five distinct perspectives that we describe in details in dedicated sections:
  * the **Modeling** perspective (the default perspective);
The Modeling perspective is dedicated to the definition of models and provides a GAML editor and an outline view of the model allowing to easily navigate through the model. It allows to run experiments.

![http://gama-platform.googlecode.com/files/modeling_perspective.png](http://gama-platform.googlecode.com/files/modeling_perspective.png)

  * the  **Simulation** perspective
The Simulation perspective allows to run the simulation and to access to the different displays, the parameter pane, and so on. Note that at least one experiment should be ran to access to the Simulation perspective.
![http://gama-platform.googlecode.com/files/simulation_perspective.png](http://gama-platform.googlecode.com/files/simulation_perspective.png)
This [page](OpenGLInterface16.md) propose a presentation of the use of OpenGL display.

  * the  **Batch** perspective
![http://gama-platform.googlecode.com/files/batch-perspective.png](http://gama-platform.googlecode.com/files/batch-perspective.png)

  * the **SVN Repository Exploring** perspective

  * the **Team Synchronizing** perspective

## Modeling/Simulation switch perspectives
GAMA offers the possibility to simply switch between the modeling and the simulation perspective by clicking on the top left button.

![http://gama-platform.googlecode.com/files/Perspective_switch.png](http://gama-platform.googlecode.com/files/Perspective_switch.png)

# <font color='blue'> Project and model creation </font>
## project creation
Before creating a model, GAMA users should create a project. This project will contain all the files necessary to run or several models. To create a project, two solutions:
  * in the GAMA projects pane, right click on the User models, then choose "New... -> Gama Project"
  * in the menu, choose "File", then "Project...". In the menu, choose "GAMA -> Gama Project" then "Next >"
![http://gama-platform.googlecode.com/files/project_creation.png](http://gama-platform.googlecode.com/files/project_creation.png)

## model creation
To create a model, two solutions exist:
  * in the GAMA projects pane, right click on one of the project of the User models, then choose "New... -> Model File"
  * in the menu, choose "File", then "Other...". In the menu, choose "GAMA -> Model file" then "Next >"
![http://gama-platform.googlecode.com/files/model_creation.png](http://gama-platform.googlecode.com/files/model_creation.png)

# <font color='blue'> Project importation </font>
GAMA allows to simply import existing projects into the workspace.
For that, just select "Import..." in the "File" menu.

![https://gama-platform.googlecode.com/svn/wiki/images/import_file.png](https://gama-platform.googlecode.com/svn/wiki/images/import_file.png)

Then, in the menu, select in "General", "Existing Projects into Workspace" and click on "Next>".

![https://gama-platform.googlecode.com/svn/wiki/images/import_menu.png](https://gama-platform.googlecode.com/svn/wiki/images/import_menu.png)

You can then choose the project to import  (from the root directory of the project or an archive file) and choose to copy or not the project to the workspace.

![https://gama-platform.googlecode.com/svn/wiki/images/import_frame.png](https://gama-platform.googlecode.com/svn/wiki/images/import_frame.png)

# <font color='blue'> Experiment running </font>
Once a model compiled (no error in the code: green color), all experiments contained in the model can be ran. To run an experiment, just click on its name. The running of a model open the Simulation perspective that allows to run the simulation.


![http://gama-platform.googlecode.com/files/run_experiment.png](http://gama-platform.googlecode.com/files/run_experiment.png)