[//]: # (keyword|operator_smooth)
[//]: # (keyword|operator_rectangle)
[//]: # (keyword|concept_3d)
[//]: # (keyword|concept_shape)
# 3D Display model of Rounded Rectangle


_Author : Arnaud Grignard_

Model presenting a 3D display of rounded rectangle


Code of the model : 

```


model rounded_rectangle   

global {
	//Parameter to define the number of agents to create
	int number_of_agents parameter: 'Number of Agents' min: 1 <- 100 category: 'Initialization';
	
	//Parameter to define the dimensions of a square environment
	int width_and_height_of_environment parameter: 'Dimensions' min: 10 <- 100 category: 'Initialization';
	
	//Parameter to define the depth of a rounded rectangle
	int elevation parameter: 'Elevation' min: 0 <- 0 ;
	
	rgb global_color;
	int maxSize;
	
	file imageRaster <- file('../images/Gama.png') ;
	
	list blueCombination <- [([0,113,188]),([68,199,244]),([157,220,249]),([212,239,252])];
	list blueNeutral <- [([0,107,145]),([211,198,173]),([241,223,183])];
	list ColorList <- [blueCombination,blueNeutral];
	
	geometry shape <- square(width_and_height_of_environment);
	init { 
		
		global_color <- #yellow;

		maxSize<- 10;
		
		create mySquare number:number_of_agents{
			width <- float(rnd(maxSize)+1);
			height <-float(rnd(maxSize)+1);		
			color <- rgb((ColorList[0])[rnd(2)]);
		}
	}  
} 

species mySquare{
	float width ;
	float height;
	rgb color;	
		
	reflex updateShape{
		width <- float(rnd(maxSize));
		height <-float(rnd(maxSize));
		color <- rgb (blueCombination[rnd(3)]);
			
	}

	aspect RoundCorner {
		//the smooth operator allows to have a high fit (near 1.0)  or low fit (near 0.0)
		draw rectangle(self.width, self.height) smooth 0.5 color: color border:color  depth:elevation; 
	}
}	
	


experiment Display  type: gui {
	output {
		display Poincare type:opengl ambient_light:50 {
			image imageRaster.path ;
			species mySquare aspect:RoundCorner transparency: 0.5 position: {0,0,0.1} ;	
												
		}
	}
}
```
