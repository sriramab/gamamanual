[//]: # (keyword|operator_cube)
[//]: # (keyword|skill_moving3D)
[//]: # (keyword|concept_grid)
[//]: # (keyword|concept_agent_movement)
# Moving cells


_Author : Arnaud Grignard_

Second part of the tutorial : Tuto3D


![F:\Gama\GamaWiki\resources\images\modelLibraryScreenshots\Tutorials\3D\3D Model 02\View1-10.png](F:\Gama\GamaWiki\resources\images\modelLibraryScreenshots\Tutorials\3D\3D Model 02\View1-10.png)

Code of the model : 

```
model Tuto3D   

global {
  int nb_cells <-100;
  int environmentSize <-100;
  geometry shape <- cube(environmentSize);	
  init { 
    create cells number: nb_cells { 
      location <- {rnd(environmentSize), rnd(environmentSize), rnd(environmentSize)};       
    } 
  }  
} 
  
species cells skills:[moving3D]{  
	
  reflex move{
  	do move;
  }	                    
  aspect default {
    draw sphere(environmentSize*0.01) color:#blue;   
  }
}

experiment Display  type: gui {
  parameter "Initial number of cells: " var: nb_cells min: 1 max: 1000 category: "Cells" ;
  output {
    display View1 type:opengl{
      graphics "env"{
      	draw cube(environmentSize) color: #black empty:true;	
      }
      species cells;
    }
  }
}
```
