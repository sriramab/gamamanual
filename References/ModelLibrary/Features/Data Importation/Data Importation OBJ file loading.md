[//]: # (keyword|concept_load_file)
[//]: # (keyword|concept_3d)
[//]: # (keyword|concept_skill)
[//]: # (keyword|concept_obj)
# Complex Object Loading


_Author :  Arnaud Grignard_

Provides a  complex geometry to agents (svg,obj or 3ds are accepted). The geometry becomes that of the agents.


![F:\Gama\GamaWiki\resources\images\modelLibraryScreenshots\Features\Data Importation\Data Importation OBJ file loading\complex-10.png](F:\Gama\GamaWiki\resources\images\modelLibraryScreenshots\Features\Data Importation\Data Importation OBJ file loading\complex-10.png)

Code of the model : 

```

model obj_loading   

global {

	init { 
		create object;
	}  
} 

species object skills:[moving]{
	
	geometry shape <- obj_file("../includes/teapot.obj") as geometry;
	
	reflex move{
		do wander;
	}
	aspect obj {
		draw shape;
	}
			
}	

experiment Display  type: gui {
	output {
		display complex  background:#gray type: opengl{
		  species object aspect:obj;				
		}
	}
}
```
