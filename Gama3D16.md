OpenGL display is now fully available in GAMA 1.6.


<a href='http://www.youtube.com/watch?feature=player_embedded&v=ycbeYxV2B7M' target='_blank'><img src='http://img.youtube.com/vi/ycbeYxV2B7M/0.jpg' width='425' height=344 /></a>

[Tutorial](http://code.google.com/p/gama-platform/wiki/Tuto3D)



# How to use OpenGL display

  * Define the attribute type of the display with "`type:opengl`" in the output of your model:
```
output {
  display DisplayName type:opengl {
    species mySpecies;
  }
```

or

  * Use the preferences windows to use opengl display by default.

# How to use Camera in an opengl display
  * Video presenting the OpenGL display and the 2 cameras :

<a href='http://www.youtube.com/watch?feature=player_embedded&v=X0WbpuU4OLg' target='_blank'><img src='http://img.youtube.com/vi/X0WbpuU4OLg/0.jpg' width='425' height=344 /></a>

**ArcBall camera Movements :**

| **Key** | **Function** |
|:--------|:-------------|
| **Double Click** | Zoom Fit     |
| **Up**  | Horizontal movement to the top|
| **Down**| Horizontal movement to the bottom|
| **Left**| Horizontal movement to the left |
| **Right**| Horizontal movement to the right|
| **<sub>SHIFT+Up</sub>**| Rotate the model up (rotation around x axis)|
| **<sub>SHIFT+Down</sub>**| Rotate the model down (rotation around x axis)|
| **<sub>SHIFT+Left</sub>**| Rotate the model left(rotation around y axis)|
| **<sub>SHIFT+Right</sub>**| Rotate the model right (rotation around y axis)|
| **<sub>ALT+Left</sub>**|   Rotate the model around z axis|
| **<sub>ALT+Right</sub>**| Rotate the model around z axis|
| **<sub>CMD+MOUSE</sub>1** | Makes the camera rotate around the model |
| **<sub>ALT+MOUSE</sub>**| Enables ROI Agent Selection |
| **<sub>SHIFT+MOUSE</sub>**| Enables ROI Zoom |
| **<sub>SCROLL</sub>**| Zoom-in/out to the current target (center of the sphere)|


**Free Fly camera Movements :**

| **Key** | **Function** |
|:--------|:-------------|
| **Double Click** | Zoom Fit     |
| **Up**  | Move forward |
| **Down**| Move backward|
| **Left**| Strafe left  |
| **Right**| Strafe right |
| **<sub>SHIFT+Up</sub>**| Look up      |
| **<sub>SHIFT+Down</sub>**| Look down    |
| **<sub>SHIFT+Left</sub>**| Look left    |
| **<sub>SHIFT+Right</sub>**| Look right   |
| **<sub>MOUSE</sub>**| Makes the camera look up, down, left and right |
| **MouseWheel**| Zoom-in/out to the current target (center of the screen)|

_1 : control button on Windows_


# Add 3D in your model


  * layer can be drawn on different z value using the position facet

```
display myDisplay type:opengl {
 species building aspect: base position:{0,0,0};
 species road aspect: base position:{0,0,0.1};
 species people aspect: base position:{0,0,0.2};
}
```

![http://gama-platform.googlecode.com/files/multi_layer_1_6.png](http://gama-platform.googlecode.com/files/multi_layer_1_6.png)

  * layer can be drawn with different transparency value
```
display myDisplay type:opengl  {
  species building aspect:base transparency:0.8;
  species road aspect: base transparency:0;
  species people aspect: base transparency:0.5;
}
```

![http://gama-platform.googlecode.com/files/transparency.png](http://gama-platform.googlecode.com/files/transparency.png)


  * When a layer represent static data it can be drawn only once at the initialisation. Use the facet refresh to specify the type of data of the layer. E.g in road traffic building are static data that do not evolve during the simulation. The display will be much more faster with this option as the geometry of the layer are computed only once and then send to the Graphic card by the use of DisplayList.
```
display myDisplay type:opengl  {
  species building aspect:base transparency:0.8;
  species road aspect: base transparency:0;
  species people aspect: base transparency:0.5 refresh:false;
}
```


# Digital Model Elevation
Some example of Digital Model Elevation Display can be found in models/3D/DEM.


# From PNG FILE
![http://gama-platform.googlecode.com/files/vulcano_dem.png](http://gama-platform.googlecode.com/files/vulcano_dem.png)
```
global{
file dem parameter: 'DEM' <- file('../includes/DEM-Vulcano/DEM.png');
file texture parameter: 'Texture' <- file('../includes/DEM-Vulcano/Texture.png');
}
```
```
display Vulcano  type: opengl ambient_light:255 {
  graphics GraphicPrimitive {
    draw dem(dem, texture);
  }
}

display VulcanoDEM  type: opengl ambient_light:255 {
  graphics GraphicPrimitive {
    draw dem(dem, dem);
  }
}
```

# From an ASC file
![http://gama-platform.googlecode.com/files/dem-example.png](http://gama-platform.googlecode.com/files/dem-example.png)
## ASC File
```
ncols         7
nrows         5
xllcorner     855931.82803726
yllcorner     6265857.3473187
cellsize      1
NODATA_value  -9999
0 1 2 3 4 5 6
5 4 3 2 1 2 3
9 8 7 6 5 4 3
0 1 2 3 4 5 6
5 4 3 2 1 2 3
```


## Loading
```
model gridloading

global {
  file grid_file <- file("../includes/asc_grid/7x5.asc");
  file map_texture parameter: 'Texture' <- file('../includes/DEM_hanoi/maps.png');
  map colors <- map([1:: hsb(0.66,0.1,0.5), 2:: hsb(0.66,0.2,0.5),3:: hsb(0.66,0.3,0.5),4:: hsb(0.66,0.4,0.5),5:: hsb(0.66,0.5,0.5),6:: hsb(0.66,0.6,0.5),7:: hsb(0.66,0.7,0.5),8:: hsb(0.66,0.8,0.5),9:: hsb(0.66,0.9,0.5),10:: hsb(0.66,1.0,0.5) ]);
  geometry shape <- envelope(grid_file);
}

entities {
  grid cell file: grid_file {
    init {
      color <- colors at int(grid_value);
    }
  }
}
```
## Display
```

display gridTextureWithGridColor type:opengl{
  grid cell;
}
display gridTextureWithFile type:opengl{
  grid cell texture:map_texture;
}
display gridTextureWithText type:opengl{
  grid cell text:true;
}
display gridNonTexturedWithDEMValue type:opengl{
  grid cell texture:false;
}	
display gridTriangulatedWithGridColor type:opengl{
  grid cell triangulation:true;
}
display gridTriangulatedWithFile type:opengl{
  grid cell texture:map_texture triangulation:true;
}
```