
<br />

# <font color='blue'>Description</font>

  * **Authors:** Simon Daudin, Marie Pietrowski, Gabriel Somogyi, Olivia Stanescu, Violaine Villebonnet
  * **Supervizer:** Benoit Gaudou / Arnaud Grignard

# <font color='blue'>Introduction</font>

The aim of the Offline Visualization Tool (OVT) is to be able to run a simulation in the GAMA environment, store it into a file and to replay it offline in a browser.

Note 1: the Offline Visualization Tool and the export of a simulation into offline visualizable file is still experimental.
To get the Offline Visualization Tool, please send me an email (benoit "." gaudou "@" gmail "." com, without spaces and ").

Note 2: **the OVT only works on Firefox**.

# <font color='blue'> Export a simulation </font>

In order to produce the file containing the simulation, modeler only has to add the following facet to the display he wants to save into a file. The pair represents the step interval that will be recorded. The first element of the pair should be 0. The display should **display species** in the **opengl mode**.

```
display city_display refresh_every: 1 type: opengl output3D: {0,10} {
.....
}
```

This will create a new folder `file3D` in the folder containing the GAML model. It will contains a file named `level.xml`. **This name should not be modified.**

Note:
  * As there could be lot of agents of each species, modeler can group them. To do that, at the end of the file, he should add a group for each species, in the `<group id="objects">` element:

```
<group id="people" name="people">
...
</group>
```

# <font color='blue'>Replay a simulation </font>

Once the `level.xml` file has been produced:
  * it should be copied in the `xml` folder of the viewer.
  * the user should open the `index.html` file into his Firefox brower.

## Interface

![http://gama-platform.googlecode.com/files/OfflineVisualizationToolInterface.png](http://gama-platform.googlecode.com/files/OfflineVisualizationToolInterface.png)

### Canvas
The canvas is the area where the 3D scene is displayed. It is possible to move the camera up,
down, right and left, to zoom in and out and to move in the scene with the mouse. The user can
click on an object into the canvas to select it and display information.

### Checkboxes
They are used to set visible or invisible the elements of the scene. There are groups of objects
like “Cars” which have an effect on all their members. At first, groups are reduced but you can
click on the “+” button to deploy the members, and then chose the visibility of a particular
object. When an element is born/dies, its checkbox appears/disappears, so it can not be modified
when it is not alive.

### Animation bar
In this part, there are buttons for pause/play the animation, go next or previous step, and reset the
simulation (go to time 0). There is also a progress bar with the actual frame of the animation. It is
here that the user can choose:
  * the speed of the simulation
  * the number of frame between two steps (Frame By Frame)
  * the sensibility (the camera speed)
  * the frame he wants to see directly. The animation then starts from this frame number.

### Information area
This is a table with all the information on the selected object (contained in the CSV file). If there
is no element selected, nothing is displayed, and if the selected element has no attribute, there is
only its ID.

## Controls

There are several keyboard and mouse controls to interact with the application :
  * ↑ ↓ or mouse wheel : zoom in/out
  * ← → : go left/right with the camera
  * Space : go up with the camera
  * Ctrl : go down with the camera
  * Mouse left button (hold it) and move : move in the scene