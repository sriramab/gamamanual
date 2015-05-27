This is a list of items that are still in developpement or open question in the field of visualization in Gama. Those technical diffculties are coming either from the topic itself or from the lack of knowledge in Gama.


# Technical (Short term)
  * Switch from jogl 1.1 to jogl 2.0 => NOT FINISHED

  * Implement JOGLSWTGLRenderer (SWT) insted of JOGLAWTGLRenderer (AWT) => NOT FINISHED

  * Picking: identify an get agent information by clicking on it => OK

  * Use Vertex Buffer Object (VBO) instead of glVertex (start maybe with DisplayList ) => NOT FINISHED

  * Enhance and finish the arcball implementation ( Skecthup arcball can be a benchmark) => OK

  * Z-fighting problem (2 coplanar polygons are not well rendered) => Still some issues




# New feature (Middle term)
  * Collada input/output  => NOT DONE
**Existing: Work in progress: ColladaReader class**
```
DrawCollada() in JOGLAWT Renderer
```

**To Do: Specify on aspect by giving a collada file**
```
file collada <- file('collada.dae') ;
...

aspect object{    		
  draw collada: collada.path;
}
```


  * Display a .shp file when clicking on it => NOT DONE

**Existing: click on button addShapeFile() in JOGLAWTDisplaySurface open a file browser and add a collection in a list of collection that are drawn with  DrawShapeFile() in JOGLAWTGLRenderer**

**To Do: call addShapeFile() when the user click on the shape file in the browser**

  * Multi level of details
**Existing: NONE**

  * graph layout
**Existing: For the time being a graph can be displayed in Gama but without any computed layout. Work done with Samuel at the coding Camp with GraphStream.**

**To Do: Compute a layout**

# Long term
  * WebGl
http://www.netmagazine.com/features/20-webgl-sites-will-blow-your-mind

http://gdd11-webgl.appspot.com/#1

http://www.aerotwist.com/tutorials/getting-started-with-three-js/
  * Interactive model
http://paperjs.org/examples/voronoi/

  * Edit agent shape "by hand"
http://paperjs.org/examples/hit-testing/

