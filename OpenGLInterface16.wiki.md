# Introduction

GAMA 1.6 proposes an OpenGL display for simulations. OpenGL display visualization allows to display a high number of agents and offers the possibility to navigate through a simulation in 3D.


# How to use OpenGL display

**Use the Toggle 3D icon to switch between 2D and 3D view**

![http://gama-platform.googlecode.com/files/3D_toggle_button.png](http://gama-platform.googlecode.com/files/3D_toggle_button.png)

**Use the Toggle Camera icon to switch between Arcball and Free Fly camera**

![http://gama-platform.googlecode.com/files/camera_toggle_button.png](http://gama-platform.googlecode.com/files/camera_toggle_button.png)

A little video presenting the OpenGL display and the 2 cameras :

<a href='http://www.youtube.com/watch?feature=player_embedded&v=X0WbpuU4OLg' target='_blank'><img src='http://img.youtube.com/vi/X0WbpuU4OLg/0.jpg' width='425' height=344 /></a>

**ArcBall camera Movements :**

| **Key** | **Function** |
|:--------|:-------------|
| **Up**  | Horizontal movement to the top|
| **Down**| Horizontal movement to the bottom|
| **Left**| Horizontal movement to the left |
| **Right**| Horizontal movement to the right|
| **<sub>SHIFT+Up</sub>1**| Rotate the model up|
| **<sub>SHIFT+Down</sub>1**| Rotate the model down|
| **<sub>SHIFT+Left</sub>1**| Rotate the model left|
| **<sub>SHIFT+Right</sub>1**| Rotate the model right|
| **<sub>SHIFT+MOUSE</sub>1** | Makes the camera rotate around the model |
| **MouseWheel**| Zoom-in/out to the current target (center of the sphere)|


**Free Fly camera Movements :**

| **Key** | **Function** |
|:--------|:-------------|
| **Up**  | Move forward |
| **Down**| Move backward|
| **Left**| Strafe left  |
| **Right**| Strafe right |
| **<sub>SHIFT+Up</sub>1**| Look up      |
| **<sub>SHIFT+Down</sub>1**| Look down    |
| **<sub>SHIFT+Left</sub>1**| Look left    |
| **<sub>SHIFT+Right</sub>1**| Look right   |
| **<sub>MOUSE</sub>1**| Makes the camera look up, down, left and right |
| **MouseWheel**| Zoom-in/out to the current target (center of the screen)|

_1 : Meta button on MAC OS X_

**Use the Select Rectangle button to select agents or zoom in a region of interest**

Using this button it is possible to select several agents at the same time. A Rectangle can be drawn which will select all the agents in the ROI, but the model has to be in 2D view. Several agents can also be selected in 3D view without drawing the ROI, but only the agents on a same location of the model.


![http://gama-platform.googlecode.com/files/select_rectangle_button.png](http://gama-platform.googlecode.com/files/select_rectangle_button.png)

**Select Rectangle mode keyboard shortcut :**

| **Key** | **Function** |
|:--------|:-------------|
| **ALT+MouseDrag**| Draw a rectangle, when mouse key is released zoom onto the region of interest|