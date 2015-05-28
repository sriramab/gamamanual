# Displays



GAMA allows modelers to [define several and several kinds of displays](G__DefiningDisplays) in a [GUI experiment](G__DefiningExperiments):
  * java 2D displays
  * OpenGL displays

These 2 kinds of display allows the modeler to display the same objects (agents, charts, texts ...). The OpenGL display offers extended features in particular in terms of 3D visualisation.
The OpenGL displays offers in addition better performance when zooming in and out.






## Classical displays (java2D)

The classical displays displaying any kind of content can be manipulated via the mouse (if no mouse event has been defined):
  * the **mouse left** press and move allows to move the camera (in 2D),
  * the **mouse right** click opens a context menu allowing the modeler to inspect displayed agents,
  * the **wheel** allows the modeler to zoom in or out.


<img src='images/experiments/display-java2D.png' />


Each display provides several buttons to manipulate the display:
  * **Pause the-display**: when pressed, the display will not be displayed anymore, the simulation is still running,
  * **Update every X step**: configure the refresh frequence of the display,
  * **Synchronize the display and the execution of the model**,
  * **Take a snapshot**: take a snapshot saved as a png image in the `snapshots` folder of the models folder,
  * **Zoom in**,
  * **Zoom to fit view**,
  * **Zoom out**,
  * **Browse through all displayed agents**: open a context menu to inspect agents,
  * **Show/hide side bar**,
  * **Show/hide overlay**.

The Show/Hide side bar button opens a side panel in the display allowing the modeler to configure:
  * **Properties** of the display: background and highlight color, display the scale bar
  * For each layer, we can configure visibility, transparency, position and size of the layer. For grid layers, we can in addition show/hide grids. For species layers, we can also configure the displayed aspect. For text layers, we can the expression displayed with the color and the font.

The bottom overlay bar displays information about the way it is displayed:
  * the position of the mouse in the display,
  * the zoom ratio,
  * the scale of the display (depending on the zoom).


<img src='images/experiments/display-sidebar-overlay.png' />






## OpenGL displays

The OpenGL display has an additional button **3D Options** providing 3D features:
  * **Use FreeFly camera**/**Use Arcball camera**: switch between cameras, the default camera is the Arcball one,
  * **Rotate scene**: rotate the scene around an axis orthogonal to the scene,
  * **Split layers**/**Merge layers**: display each layer at a distinct height,
  * **Triangulate scene**
  * **Arcball drag** (only with Arcball camera): the right press and hold and mouse move makes rotation on the scene
  * **Inertia mode** (only with Arcball camera): in inertia mode, when the modeler stops moving the camera, there is no straight halt but a kind of inertia.


<img src='images/experiments/display-OpenGL.png' />


In addition, the bottom overlay bar provides the Camera position in 3D.