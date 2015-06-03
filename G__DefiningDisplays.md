
# Defining Displays







A display refers to a independent and mobile part of the interface that can display species, images, texts or charts.

The general syntax is:
```
display my_display [additional options] { ... }
```

Additional options include:
  * **`background`** (type = color): the color of the display background
  * **`type`** (2 possible values: java2D or opengl): specify if the display will use the java 2D ou openGL libraries. Note that the openGl display does not admit charts. The default value is java2D.
  * **`refresh_every`** (type = int): the display will be refreshed every nb steps of the simulation
  * **`autosave`** (type = boolean or location): if the value is true or is a location, GAMA will take each a snapshot of the display every time the display is refreshed. The location will precise the dimaension of the picture.


There exist several kinds of display:
  * classical **displays** (without specific type) used to species, text, image, charts...
```
display my_display { ... }
```
  * **opengl displays** (display with `type: opengl`) used to display species, text or image. It allows to display 3D models.
```
display my_display type: opengl { ... }
```

Each display can be refreshed independently by defining the facet **refresh\_every: nb (int)** (the display will be refreshed every nb steps of the simulation)

Each display can include different layers (like in a GIS). Although every combinaison of any number of following layers are allowed in GAML, it is recommended to distinguish displays with species, image and/or text and display with charts (and text).
