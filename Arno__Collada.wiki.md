# Accessing Digital Assets for Three-Dimensional Rendering.

Ref ([dyn-lab.com](http://www.dyn-lab.com/articles/collada-and-opengl.html))


Collada is a file format for storing 3-D digital content is the open-source COLLADA (Collaborative Design Activity) format

OpenGL rendering is based on vertices—three-dimensional points. Collada files contain coordinates, colors, and normal vectors associated with vertices. The section shows how to parse XML to acces COLLADA's vertex information.

# References

[Tutorial](http://www.wazim.com/Collada_Tutorial_1.htm)

# Collada format

A COLLADA mesh provides information about the vertices of an object
  * 3-D coordinates to identify  vertices location
  * Normal vector for each vertex
  * Description of how vertices must be connected to form the object

```
<COLLADA>
   ...
   <library_geometries>
      <geometry>
         <mesh>
         ...
         </mesh>
      </geometry>
   </library_geometries>
   ...
</COLLADA>
```


`<library_geometries>` (`<COLLADA>` child) contains a `<geometry>` element for each object in the model.

The `<geometry>` element contains the `<mesh>` element, which holds the vertex data needed to render an object in the model.

## `<source>`
```
<source id="ID5">
   <float_array id="ID8" count="798">-5.551e-017 -2.608...</float_array>
   <technique_common>
      <accessor count="266" source="#ID8" stride="3">
      ...
      </accessor>
   </technique_common>
</source>
```


`<float_array>` contains 798 floating-point values. (could be `<int_array>`, `<bool_array>`, or `<name_array>`).

`<source>` element contains a `<technique_common>` to identify how to acces data. `<accessor>` states that the floating-point data should be accessed in groups of three (stride) and that the array contains 266 such groups (count).


## `<vertices>`


File contains two `<source>` elements: one whose ID equals ID5 and one whose ID equals ID6.
```
<vertices id="ID7">
   <input semantic="POSITION" source="#ID5" />
   <input semantic="NORMAL" source="#ID6" />
</vertices>
```

The semantic attribute identifies the meaning of the data inside the two `<source>` elements. In this file, the `<source>` element whose ID equals ID5 contains position information (POSITION). The `<source>` element whose ID equals ID6 contains normal vector components (NORMAL). Other values of the semantic attribute include COLOR, TEXCOORD, TEXTURE, TANGENT, BINORMAL, and UV.

Before we can use this data to render the object, we need to know how the vertices are combined into the basic shapes that define a three-dimensional object. These basic shapes, called primitives, include lines, triangles, and polygons. This information is provided by the `<triangles> element`.

## `<triangles>`

```
<triangles count="528" material="Material2">
   <input offset="0" semantic="VERTEX" source="#ID7" />
   <p>0 1 2 1 0 3...</p>
</triangles>
```




The count attribute states that there are 528 triangles and the material attribute identifies the material to be applied to each triangle.

The `<p>` element identifies how each vertex should be reused within each triangle. In sphere.dae, the first triangle consists of Vertex 0, Vertex 1, and Vertex 2. The second triangle consists of Vertex 1, Vertex 0, and Vertex 3. The orientation is important—OpenGL culls polygons according to whether their vertices are given in clockwise or counter-clockwise order.

# Implementation

Use [ColladaImporter](http://home.adelphi.edu/~stemkoski/jme2/javadoc/com/jmex/model/collada/ColladaImporter.html)

ColladaNode provides a mechanism to parse and load a COLLADA (COLLAborative Design Activity) model. Making use of a DOM parse, the XML formatted COLLADA file is parsed into Java Type classes and then processed by jME. This processing is currently aimed at the 1.4.1 release of the COLLADA Specification, and will, in most likelihood, require updating with a new release of COLLADA.


In `msi.gama.ext/jme-collada.jar`