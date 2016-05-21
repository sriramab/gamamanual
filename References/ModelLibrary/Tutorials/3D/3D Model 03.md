[//]: # (keyword|operator_cube)
[//]: # (keyword|operator_select)
[//]: # (keyword|skill_moving3D)
[//]: # (keyword|concept_3d)
[//]: # (keyword|concept_light)
[//]: # (keyword|concept_grid)
[//]: # (keyword|concept_neighbors)
# Moving cells with neighbors


_Author : Arnaud Grignard_

Third part of the tutorial : Tuto3D


Code of the model : 

```

model Tuto3D

global {
	geometry shape <- cube(100);
	init { 
		create cells number: 1000{ 
			location <- {rnd(100), rnd(100), rnd(100)};	
		} 
	}  
} 
    
species cells skills: [moving3D] {  
	rgb color;
	list<cells> neighbors;
	int offset;
	
	reflex move {
      do wander;	
	}	
	
	reflex computeNeighbors {
      neighbors <- cells select ((each distance_to self) < 10);
    }
		
	aspect default {
		draw sphere(10) color:#orange;
		loop pp over: neighbors {
			draw line([self.location,pp.location]);
		}	
    }
}

experiment Display  type: gui {
	output {
		display View1 type:opengl background:rgb(10,40,55) {
			species cells aspect: default;
		}
	}
}


```
