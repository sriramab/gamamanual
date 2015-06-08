# Extension

----
 cenres.gaml.extensions.hydro

## Table of Contents
### Operators
[water_area_for](#water_area_for), [water_level_for](#water_level_for), [water_polylines_for](#water_polylines_for), 

### Statements


### Skills


### Architectures



### Species



----

## Operators
	
----

### `water_area_for`
* **Possible use:** 
  * geometry OP float --->  float
* **Special cases:**     
  * if the left operand is a polyline and the right operand a float for the water y coordinate, returrns the area of the water (water flow area)
* **Examples:** 

```
waterarea <- my_river_polyline water_area_for my_height_value

```

  

[Top of the page](#table-of-contents)
  	
----

### `water_level_for`
* **Possible use:** 
  * geometry OP float --->  float
* **Special cases:**     
  * if the left operand is a polyline and the right operand a float for the area, returrns the y coordinate of the water (water level)
* **Examples:** 

```
waterlevel <- my_river_polyline water_level_for my_area_value

```

  

[Top of the page](#table-of-contents)
  	
----

### `water_polylines_for`
* **Possible use:** 
  * geometry OP float --->  msi.gama.util.IList<msi.gama.util.IList<msi.gama.metamodel.shape.GamaPoint>>
* **Special cases:**     
  * if the left operand is a polyline and the right operand a float for the water y coordinate, returrns the shapes of the river sections (list of list of points)
* **Examples:** 

```
waterarea <- my_river_polyline water_area_for my_height_value

```

  

[Top of the page](#table-of-contents)
  	

----

## Skills
	

----

## Statements
		
	
----

## Species
	
	
----

## Architectures 
	