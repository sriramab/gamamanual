



# Wandering Sphere

## Model 1: 3D world made of cells

[Model 01.gaml](https://code.google.com/p/gama-platform/source/browse/branches/GAMA_CURRENT/msi.gama.models/models/Tutorials/3D/models/Model%2001.gaml)

Initialize a 3D world with a population of cells placed randomly in a 3D 100x100x100 cube.



![https://gama-platform.googlecode.com/svn/wiki/images/3D_model_LQ.png](https://gama-platform.googlecode.com/svn/wiki/images/3D_model_LQ.png)


## Model 2: Moving cells

[model2.gaml](https://code.google.com/p/gama-platform/source/browse/branches/GAMA_CURRENT/msi.gama.models/models/Tutorials/3D/models/model2.gaml)

<a href='http://www.youtube.com/watch?feature=player_embedded&v=_QqUbC0MWRU' target='_blank'><img src='http://img.youtube.com/vi/_QqUbC0MWRU/0.jpg' width='425' height=344 /></a>

Just add a moving skills to the cells

```
species cells skills:[moving]
```

and make them move with a reflex using the action **wander\_3D**

```
reflex move{
  do wander_3D;
}
```

## Model 3: Compute neighborhood and make it look nicer

<a href='http://www.youtube.com/watch?feature=player_embedded&v=6ZlBU6xTcfw' target='_blank'><img src='http://img.youtube.com/vi/6ZlBU6xTcfw/0.jpg' width='425' height=344 /></a>

### Color
**Change the background color (white by default)
```
display View1 type:opengl background:rgb(10,40,55) {
  species cells;
}
```**

**Change the color of the sphere
```
draw sphere(1) color:rgb('orange');
```**

NB: GAML allows to use the named colors declared in CSS http://www.cssportal.com/css3-color-names/.

### Neighborhood

  * Get Neighborhood
# Inside the species cells declare a new variable _neighbours_ that will contain all the neighborhood cells
```
list<cells> neighbours;
```
# Define a reflex that will compute this neighborhood by returning all the cell situated at a distance lower than 10.
```
reflex computeNeighbours {
      neighbours <- cells select ((each distance_to self) < 10);
    }
```
# Display the link by simply drawing a line between the cell and its neighborhood in the aspect of the cell.
```
loop pp over: neighbours {
  draw line([self.location,pp.location]);
}	

```



# Augmented SIR

[Augmented SIR](http://code.google.com/p/gama-platform/wiki/AugmentedSIR)

# Procedural City

[Procedural\_City.gaml](https://code.google.com/p/gama-platform/source/browse/branches/GAMA_CURRENT/msi.gama.models/models/Features/3D%20Visualization/3D%20Shapes/Procedural%20City.gaml)



<a href='http://www.youtube.com/watch?feature=player_embedded&v=t4FcZp5FbCg' target='_blank'><img src='http://img.youtube.com/vi/t4FcZp5FbCg/0.jpg' width='425' height=344 /></a>






