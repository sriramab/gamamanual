# Operators (I to M)
 	

    	
----

[//]: # (keyword|operator_IDW)
### `IDW`

#### Possible use: 
  *  **`IDW`** (`container<agent>`, `map<point,float>`, `int`) --->  `map<agent,float>` 

#### Result: 
Inverse Distance Weighting (IDW) is a type of deterministic method for multivariate interpolation with a known scattered set of points. The assigned values to each geometry are calculated with a weighted average of the values available at the known points. See: http://en.wikipedia.org/wiki/Inverse_distance_weighting Usage: IDW (list of geometries, map of points (key: point, value: value), power parameter)

#### Examples: 
```
 
map<agent,float> var0 <- IDW([ag1, ag2, ag3, ag4, ag5],[{10,10}::25.0, {10,80}::10.0, {100,10}::15.0], 2); // var0 equals for example, can return [ag1::12.0, ag2::23.0,ag3::12.0,ag4::14.0,ag5::17.0]

```
  
    	
----

[//]: # (keyword|operator_image_file)
### `image_file`

#### Possible use: 
  *  **`image_file`** (`string`) --->  `file` 

#### Result: 
Constructs a file of type image. Allowed extensions are limited to tiff, jpg, jpeg, png, pict, bmp
    	
----

[//]: # (keyword|operator_improved_generator)
### `improved_generator`

#### Possible use: 
  *  **`improved_generator`** (`float`, `float`, `float`, `float`) --->  `float` 

#### Result: 
take a x, y, z and a bias parameters and gives a value

#### Examples: 
```
 
float var0 <- improved_generator(2,3,4,253); // var0 equals 10.2

```
  
    	
----

[//]: # (keyword|operator_in)
### `in`

#### Possible use: 
  * `unknown` **`in`** `container` --->  `bool`
  *  **`in`** (`unknown` , `container`) --->  `bool`
  * `string` **`in`** `string` --->  `bool`
  *  **`in`** (`string` , `string`) --->  `bool` 

#### Result: 
true if the right operand contains the left operand, false otherwise  

#### Comment: 
the definition of in depends on the container

#### Special cases:     
  * if the right operand is nil or empty, in returns false    
  * if both operands are strings, returns true if the left-hand operand patterns is included in to the right-hand string;

#### Examples: 
```
 
bool var0 <- 2 in [1,2,3,4,5,6]; // var0 equals true 
bool var1 <- 7 in [1,2,3,4,5,6]; // var1 equals false 
bool var2 <- 3 in [1::2, 3::4, 5::6]; // var2 equals false 
bool var3 <- 6 in [1::2, 3::4, 5::6]; // var3 equals true 
bool var4 <-  'bc' in 'abcded'; // var4 equals true

```
      


#### See also: 

[contains](operators-b-to-c#contains), 
    	
----

[//]: # (keyword|operator_in_degree_of)
### `in_degree_of`

#### Possible use: 
  * `graph` **`in_degree_of`** `unknown` --->  `int`
  *  **`in_degree_of`** (`graph` , `unknown`) --->  `int` 

#### Result: 
returns the in degree of a vertex (right-hand operand) in the graph given as left-hand operand.

#### Examples: 
```
 
int var1 <- graphFromMap in_degree_of (node(3)); // var1 equals 2

```
      


#### See also: 

[out_degree_of](operators-n-to-r#out_degree_of), [degree_of](operators-d-to-h#degree_of), 
    	
----

[//]: # (keyword|operator_in_edges_of)
### `in_edges_of`

#### Possible use: 
  * `graph` **`in_edges_of`** `unknown` --->  `list`
  *  **`in_edges_of`** (`graph` , `unknown`) --->  `list` 

#### Result: 
returns the list of the in-edges of a vertex (right-hand operand) in the graph given as left-hand operand.

#### Examples: 
```
 
list var1 <- graphFromMap in_edges_of node({12,45}); // var1 equals [LineString]

```
      


#### See also: 

[out_edges_of](operators-n-to-r#out_edges_of), 
    	
----

[//]: # (keyword|operator_incomplete_beta)
### `incomplete_beta`

#### Possible use: 
  *  **`incomplete_beta`** (`float`, `float`, `float`) --->  `float` 

#### Result: 
Returns the regularized integral of the beta function with arguments a and b, from zero to x.
    	
----

[//]: # (keyword|operator_incomplete_gamma)
### `incomplete_gamma`

#### Possible use: 
  * `float` **`incomplete_gamma`** `float` --->  `float`
  *  **`incomplete_gamma`** (`float` , `float`) --->  `float` 

#### Result: 
Returns the regularized integral of the Gamma function with argument a to the integration end point x.
    	
----

[//]: # (keyword|operator_incomplete_gamma_complement)
### `incomplete_gamma_complement`

#### Possible use: 
  * `float` **`incomplete_gamma_complement`** `float` --->  `float`
  *  **`incomplete_gamma_complement`** (`float` , `float`) --->  `float` 

#### Result: 
Returns the complemented regularized incomplete Gamma function of the argument a and integration start point x.
    	
----

[//]: # (keyword|operator_indented_by)
### `indented_by`

#### Possible use: 
  * `string` **`indented_by`** `int` --->  `string`
  *  **`indented_by`** (`string` , `int`) --->  `string` 

#### Result: 
Converts a (possibly multiline) string by indenting it by a number -- specified by the second operand -- of tabulations to the right
    	
----

[//]: # (keyword|operator_index_by)
### `index_by`

#### Possible use: 
  * `container` **`index_by`** `any expression` --->  `map`
  *  **`index_by`** (`container` , `any expression`) --->  `map` 

#### Result: 
produces a new map from the evaluation of the right-hand operand for each element of the left-hand operand

#### Special cases:     
  * if the left-hand operand is nil, index_by throws an error. If the operation results in duplicate keys, only the first value corresponding to the key is kept

#### Examples: 
```
 
map var0 <- [1,2,3,4,5,6,7,8] index_by (each - 1); // var0 equals [0::1, 1::2, 2::3, 3::4, 4::5, 5::6, 6::7, 7::8]

```
  
    	
----

[//]: # (keyword|operator_index_of)
### `index_of`

#### Possible use: 
  * `map` **`index_of`** `unknown` --->  `unknown`
  *  **`index_of`** (`map` , `unknown`) --->  `unknown`
  * `species` **`index_of`** `unknown` --->  `int`
  *  **`index_of`** (`species` , `unknown`) --->  `int`
  * `string` **`index_of`** `string` --->  `int`
  *  **`index_of`** (`string` , `string`) --->  `int`
  * `matrix` **`index_of`** `unknown` --->  `point`
  *  **`index_of`** (`matrix` , `unknown`) --->  `point`
  * `list` **`index_of`** `unknown` --->  `int`
  *  **`index_of`** (`list` , `unknown`) --->  `int` 

#### Result: 
the index of the first occurence of the right operand in the left operand container
the index of the first occurence of the right operand in the left operand container  

#### Comment: 
The definition of index_of and the type of the index depend on the container

#### Special cases:     
  * if the left operand is a map, index_of returns the index of a value or nil if the value is not mapped    
  * if the left operator is a species, returns the index of an agent in a species. If the argument is not an agent of this species, returns -1. Use int(agent) instead    
  * if both operands are strings, returns the index within the left-hand string of the first occurrence of the given right-hand string 
  
```
 
int var1 <-  "abcabcabc" index_of "ca"; // var1 equals 2
``` 

    
  * if the left operand is a matrix, index_of returns the index as a point 
  
```
 
point var2 <- matrix([[1,2,3],[4,5,6]]) index_of 4; // var2 equals {1.0,0.0}
``` 

    
  * if the left operand is a list, index_of returns the index as an integer 
  
```
 
int var3 <- [1,2,3,4,5,6] index_of 4; // var3 equals 3 
int var4 <- [4,2,3,4,5,4] index_of 4; // var4 equals 0
``` 



#### Examples: 
```
 
unknown var0 <- [1::2, 3::4, 5::6] index_of 4; // var0 equals 3

```
      


#### See also: 

[at](operators-a-to-a#at), [last_index_of](operators-i-to-m#last_index_of), 
    	
----

[//]: # (keyword|operator_inside)
### `inside`

#### Possible use: 
  * `container<agent>` **`inside`** `geometry` --->  `list<geometry>`
  *  **`inside`** (`container<agent>` , `geometry`) --->  `list<geometry>` 

#### Result: 
A list of agents or geometries among the left-operand list, species or meta-population (addition of species), covered by the operand (casted as a geometry).

#### Examples: 
```
 
list<geometry> var0 <- [ag1, ag2, ag3] inside(self); // var0 equals the agents among ag1, ag2 and ag3 that are covered by the shape of the right-hand argument. 
list<geometry> var1 <- (species1 + species2) inside (self); // var1 equals the agents among species species1 and species2 that are covered by the shape of the right-hand argument.

```
      


#### See also: 

[neighbors_at](operators-n-to-r#neighbors_at), [neighbors_of](operators-n-to-r#neighbors_of), [closest_to](operators-b-to-c#closest_to), [overlapping](operators-n-to-r#overlapping), [agents_overlapping](operators-a-to-a#agents_overlapping), [agents_inside](operators-a-to-a#agents_inside), [agent_closest_to](operators-a-to-a#agent_closest_to), 
    	
----

[//]: # (keyword|operator_int)
### `int`

#### Possible use: 
  *  **`int`** (`any`) --->  `int` 

#### Result: 
Casts the operand into the type int
    	
----

[//]: # (keyword|operator_inter)
### `inter`

#### Possible use: 
  * `container` **`inter`** `container` --->  `list`
  *  **`inter`** (`container` , `container`) --->  `list`
  * `geometry` **`inter`** `geometry` --->  `geometry`
  *  **`inter`** (`geometry` , `geometry`) --->  `geometry` 

#### Result: 
the intersection of the two operands
A geometry resulting from the intersection between the two geometries  

#### Comment: 
both containers are transformed into sets (so without duplicated element, cf. remove_deplicates operator) before the set intersection is computed.

#### Special cases:     
  * if an operand is a graph, it will be transformed into the set of its nodes    
  * returns nil if one of the operands is nil    
  * if an operand is a map, it will be transformed into the set of its values 
  
```
 
list var0 <- [1::2, 3::4, 5::6] inter [2,4]; // var0 equals [2,4] 
list var1 <- [1::2, 3::4, 5::6] inter [1,3]; // var1 equals []
``` 

    
  * if an operand is a matrix, it will be transformed into the set of the lines 
  
```
 
list var2 <- matrix([[3,2,1],[4,5,4]]) inter [3,4]; // var2 equals [3,4]
``` 



#### Examples: 
```
 
list var3 <- [1,2,3,4,5,6] inter [2,4]; // var3 equals [2,4] 
list var4 <- [1,2,3,4,5,6] inter [0,8]; // var4 equals [] 
geometry var5 <- square(10) inter circle(5); // var5 equals circle(5)

```
      


#### See also: 

[remove_duplicates](operators-n-to-r#remove_duplicates), [union](operators-s-to-z#union), [+](operators-a-to-a#+), [-](operators-a-to-a#-), 
    	
----

[//]: # (keyword|operator_interleave)
### `interleave`

#### Possible use: 
  *  **`interleave`** (`container`) --->  `list` 

#### Result: 
a new list containing the interleaved elements of the containers contained in the operand  

#### Comment: 
the operand should be a list of lists of elements. The result is a list of elements.

#### Examples: 
```
 
list var0 <- interleave([1,2,4,3,5,7,6,8]); // var0 equals [1,2,4,3,5,7,6,8] 
list var1 <- interleave([['e11','e12','e13'],['e21','e22','e23'],['e31','e32','e33']]); // var1 equals ['e11','e21','e31','e12','e22','e32','e13','e23','e33']

```
  
    	
----

[//]: # (keyword|operator_internal_at)
### `internal_at`

#### Possible use: 
  * `agent` **`internal_at`** `list` --->  `unknown`
  *  **`internal_at`** (`agent` , `list`) --->  `unknown`
  * `container<KeyType,ValueType>` **`internal_at`** `list<KeyType>` --->  `ValueType`
  *  **`internal_at`** (`container<KeyType,ValueType>` , `list<KeyType>`) --->  `ValueType`
  * `geometry` **`internal_at`** `list` --->  `unknown`
  *  **`internal_at`** (`geometry` , `list`) --->  `unknown` 

#### Result: 
For internal use only. Corresponds to the implementation, for agents, of the access to containers with [index]
For internal use only. Corresponds to the implementation of the access to containers with [index]
For internal use only. Corresponds to the implementation, for geometries, of the access to containers with [index]    


#### See also: 

[at](operators-a-to-a#at), 
    	
----

[//]: # (keyword|operator_internal_integrated_value)
### `internal_integrated_value`

#### Possible use: 
  * `any expression` **`internal_integrated_value`** `any expression` --->  `list`
  *  **`internal_integrated_value`** (`any expression` , `any expression`) --->  `list` 

#### Result: 
For internal use only. Corresponds to the implementation, for agents, of the access to containers with [index]
    	
----

[//]: # (keyword|operator_internal_zero_order_equation)
### `internal_zero_order_equation`

#### Possible use: 
  *  **`internal_zero_order_equation`** (`any expression`) --->  `float` 

#### Result: 
An internal placeholder function
    	
----

[//]: # (keyword|operator_intersection)
### `intersection`
   Same signification as [inter](operators-i-to-m#inter)
    	
----

[//]: # (keyword|operator_intersects)
### `intersects`

#### Possible use: 
  * `geometry` **`intersects`** `geometry` --->  `bool`
  *  **`intersects`** (`geometry` , `geometry`) --->  `bool` 

#### Result: 
A boolean, equal to true if the left-geometry (or agent/point) intersects the right-geometry (or agent/point).

#### Special cases:     
  * if one of the operand is null, returns false.

#### Examples: 
```
 
bool var0 <- square(5) intersects {10,10}; // var0 equals false

```
      


#### See also: 

[disjoint_from](operators-d-to-h#disjoint_from), [crosses](operators-b-to-c#crosses), [overlaps](operators-n-to-r#overlaps), [partially_overlaps](operators-n-to-r#partially_overlaps), [touches](operators-s-to-z#touches), 
    	
----

[//]: # (keyword|operator_inverse)
### `inverse`

#### Possible use: 
  *  **`inverse`** (`matrix`) --->  `matrix<float>` 

#### Result: 
The inverse matrix of the given matrix. If no inverse exists, returns a matrix that has properties that resemble that of an inverse.

#### Examples: 
```
 
matrix<float> var0 <- inverse(matrix([[4,3],[3,2]])); // var0 equals matrix([[-2.0,3.0],[3.0,-4.0]])

```
  
    	
----

[//]: # (keyword|operator_inverse_distance_weighting)
### `inverse_distance_weighting`
   Same signification as [IDW](operators-i-to-m#IDW)
    	
----

[//]: # (keyword|operator_is)
### `is`

#### Possible use: 
  * `unknown` **`is`** `any expression` --->  `bool`
  *  **`is`** (`unknown` , `any expression`) --->  `bool` 

#### Result: 
returns true if the left operand is of the right operand type, false otherwise

#### Examples: 
```
 
bool var0 <- 0 is int; // var0 equals true 
bool var1 <- an_agent is node; // var1 equals true 
bool var2 <- 1 is float; // var2 equals false

```
  
    	
----

[//]: # (keyword|operator_is_csv)
### `is_csv`

#### Possible use: 
  *  **`is_csv`** (`any`) --->  `bool` 

#### Result: 
Tests whether the operand is a csv file.
    	
----

[//]: # (keyword|operator_is_dxf)
### `is_dxf`

#### Possible use: 
  *  **`is_dxf`** (`any`) --->  `bool` 

#### Result: 
Tests whether the operand is a dxf file.
    	
----

[//]: # (keyword|operator_is_error)
### `is_error`

#### Possible use: 
  *  **`is_error`** (`any expression`) --->  `bool` 

#### Result: 
Returns whether or not the argument raises an error when evaluated
    	
----

[//]: # (keyword|operator_is_finite)
### `is_finite`

#### Possible use: 
  *  **`is_finite`** (`float`) --->  `bool` 

#### Result: 
Returns whether the argument is a finite number or not

#### Examples: 
```
 
bool var0 <- is_finite(4.66); // var0 equals true 
bool var1 <- is_finite(#infinity); // var1 equals false

```
  
    	
----

[//]: # (keyword|operator_is_gaml)
### `is_gaml`

#### Possible use: 
  *  **`is_gaml`** (`any`) --->  `bool` 

#### Result: 
Tests whether the operand is a gaml file.
    	
----

[//]: # (keyword|operator_is_geojson)
### `is_geojson`

#### Possible use: 
  *  **`is_geojson`** (`any`) --->  `bool` 

#### Result: 
Tests whether the operand is a geojson file.
    	
----

[//]: # (keyword|operator_is_gif)
### `is_gif`

#### Possible use: 
  *  **`is_gif`** (`any`) --->  `bool` 

#### Result: 
Tests whether the operand is a gif file.
    	
----

[//]: # (keyword|operator_is_gml)
### `is_gml`

#### Possible use: 
  *  **`is_gml`** (`any`) --->  `bool` 

#### Result: 
Tests whether the operand is a gml file.
    	
----

[//]: # (keyword|operator_is_grid)
### `is_grid`

#### Possible use: 
  *  **`is_grid`** (`any`) --->  `bool` 

#### Result: 
Tests whether the operand is a grid file.
    	
----

[//]: # (keyword|operator_is_image)
### `is_image`

#### Possible use: 
  *  **`is_image`** (`any`) --->  `bool` 

#### Result: 
Tests whether the operand is a image file.
    	
----

[//]: # (keyword|operator_is_json)
### `is_json`

#### Possible use: 
  *  **`is_json`** (`any`) --->  `bool` 

#### Result: 
Tests whether the operand is a json file.
    	
----

[//]: # (keyword|operator_is_number)
### `is_number`

#### Possible use: 
  *  **`is_number`** (`float`) --->  `bool`
  *  **`is_number`** (`string`) --->  `bool` 

#### Result: 
Returns whether the argument is a real number or not
tests whether the operand represents a numerical value  

#### Comment: 
Note that the symbol . should be used for a float value (a string with , will not be considered as a numeric value). Symbols e and E are also accepted. A hexadecimal value should begin with #.

#### Examples: 
```
 
bool var0 <- is_number(4.66); // var0 equals true 
bool var1 <- is_number(#infinity); // var1 equals true 
bool var2 <- is_number(#nan); // var2 equals false 
bool var3 <- is_number("test"); // var3 equals false 
bool var4 <- is_number("123.56"); // var4 equals true 
bool var5 <- is_number("-1.2e5"); // var5 equals true 
bool var6 <- is_number("1,2"); // var6 equals false 
bool var7 <- is_number("#12FA"); // var7 equals true

```
  
    	
----

[//]: # (keyword|operator_is_obj)
### `is_obj`

#### Possible use: 
  *  **`is_obj`** (`any`) --->  `bool` 

#### Result: 
Tests whether the operand is a obj file.
    	
----

[//]: # (keyword|operator_is_osm)
### `is_osm`

#### Possible use: 
  *  **`is_osm`** (`any`) --->  `bool` 

#### Result: 
Tests whether the operand is a osm file.
    	
----

[//]: # (keyword|operator_is_pgm)
### `is_pgm`

#### Possible use: 
  *  **`is_pgm`** (`any`) --->  `bool` 

#### Result: 
Tests whether the operand is a pgm file.
    	
----

[//]: # (keyword|operator_is_property)
### `is_property`

#### Possible use: 
  *  **`is_property`** (`any`) --->  `bool` 

#### Result: 
Tests whether the operand is a property file.
    	
----

[//]: # (keyword|operator_is_R)
### `is_R`

#### Possible use: 
  *  **`is_R`** (`any`) --->  `bool` 

#### Result: 
Tests whether the operand is a R file.
    	
----

[//]: # (keyword|operator_is_saved_simulation)
### `is_saved_simulation`

#### Possible use: 
  *  **`is_saved_simulation`** (`any`) --->  `bool` 

#### Result: 
Tests whether the operand is a saved_simulation file.
    	
----

[//]: # (keyword|operator_is_shape)
### `is_shape`

#### Possible use: 
  *  **`is_shape`** (`any`) --->  `bool` 

#### Result: 
Tests whether the operand is a shape file.
    	
----

[//]: # (keyword|operator_is_skill)
### `is_skill`

#### Possible use: 
  * `unknown` **`is_skill`** `string` --->  `bool`
  *  **`is_skill`** (`unknown` , `string`) --->  `bool` 

#### Result: 
returns true if the left operand is an agent whose species implements the right-hand skill name

#### Examples: 
```
 
bool var0 <- agentA is_skill 'moving'; // var0 equals true

```
  
    	
----

[//]: # (keyword|operator_is_svg)
### `is_svg`

#### Possible use: 
  *  **`is_svg`** (`any`) --->  `bool` 

#### Result: 
Tests whether the operand is a svg file.
    	
----

[//]: # (keyword|operator_is_text)
### `is_text`

#### Possible use: 
  *  **`is_text`** (`any`) --->  `bool` 

#### Result: 
Tests whether the operand is a text file.
    	
----

[//]: # (keyword|operator_is_threeds)
### `is_threeds`

#### Possible use: 
  *  **`is_threeds`** (`any`) --->  `bool` 

#### Result: 
Tests whether the operand is a threeds file.
    	
----

[//]: # (keyword|operator_is_URL)
### `is_URL`

#### Possible use: 
  *  **`is_URL`** (`any`) --->  `bool` 

#### Result: 
Tests whether the operand is a URL file.
    	
----

[//]: # (keyword|operator_is_warning)
### `is_warning`

#### Possible use: 
  *  **`is_warning`** (`any expression`) --->  `bool` 

#### Result: 
Returns whether or not the argument raises a warning when evaluated
    	
----

[//]: # (keyword|operator_is_xml)
### `is_xml`

#### Possible use: 
  *  **`is_xml`** (`any`) --->  `bool` 

#### Result: 
Tests whether the operand is a xml file.
    	
----

[//]: # (keyword|operator_json_file)
### `json_file`

#### Possible use: 
  *  **`json_file`** (`string`) --->  `file` 

#### Result: 
Constructs a file of type json. Allowed extensions are limited to json
    	
----

[//]: # (keyword|operator_kappa)
### `kappa`

#### Possible use: 
  *  **`kappa`** (`list`, `list`, `list`) --->  `float`
  *  **`kappa`** (`list`, `list`, `list`, `list`) --->  `float` 

#### Result: 
kappa indicator for 2 map comparisons: kappa(list_vals1,list_vals2,categories, weights). Reference: Cohen, J. A coefficient of agreement for nominal scales. Educ. Psychol. Meas. 1960, 20. 
kappa indicator for 2 map comparisons: kappa(list_vals1,list_vals2,categories). Reference: Cohen, J. A coefficient of agreement for nominal scales. Educ. Psychol. Meas. 1960, 20.

#### Examples: 
```
kappa([cat1,cat1,cat2,cat3,cat2],[cat2,cat1,cat2,cat1,cat2],[cat1,cat2,cat3], [1.0, 2.0, 3.0, 1.0, 5.0]) kappa([cat1,cat1,cat2,cat3,cat2],[cat2,cat1,cat2,cat1,cat2],[cat1,cat2,cat3])  
float var2 <- kappa([1,3,5,1,5],[1,1,1,1,5],[1,3,5]); // var2 equals the similarity between 0 and 1 
float var3 <- kappa([1,1,1,1,5],[1,1,1,1,5],[1,3,5]); // var3 equals 1.0

```
  
    	
----

[//]: # (keyword|operator_kappa_sim)
### `kappa_sim`

#### Possible use: 
  *  **`kappa_sim`** (`list`, `list`, `list`, `list`) --->  `float`
  *  **`kappa_sim`** (`list`, `list`, `list`, `list`, `list`) --->  `float` 

#### Result: 
kappa simulation indicator for 2 map comparisons: kappa(list_valsInits,list_valsObs,list_valsSim, categories). Reference: van Vliet, J., Bregt, A.K. & Hagen-Zanker, A. (2011). Revisiting Kappa to account for change in the accuracy assessment of land-use change models, Ecological Modelling 222(8).
kappa simulation indicator for 2 map comparisons: kappa(list_valsInits,list_valsObs,list_valsSim, categories, weights). Reference: van Vliet, J., Bregt, A.K. & Hagen-Zanker, A. (2011). Revisiting Kappa to account for change in the accuracy assessment of land-use change models, Ecological Modelling 222(8)

#### Examples: 
```
kappa([cat1,cat1,cat2,cat2,cat2],[cat2,cat1,cat2,cat1,cat3],[cat2,cat1,cat2,cat3,cat3], [cat1,cat2,cat3]) kappa([cat1,cat1,cat2,cat2,cat2],[cat2,cat1,cat2,cat1,cat3],[cat2,cat1,cat2,cat3,cat3], [cat1,cat2,cat3],[1.0, 2.0, 3.0, 1.0, 5.0]) 

```
  
    	
----

[//]: # (keyword|operator_kmeans)
### `kmeans`

#### Possible use: 
  * `list` **`kmeans`** `int` --->  `list<list>`
  *  **`kmeans`** (`list` , `int`) --->  `list<list>`
  *  **`kmeans`** (`list`, `int`, `int`) --->  `list<list>` 

#### Result: 
returns the list of clusters (list of instance indices) computed with the kmeans++ algorithm from the first operand data according to the number of clusters to split the data into (k) and the maximum number of iterations to run the algorithm for (If negative, no maximum will be used) (maxIt). Usage: kmeans(data,k,maxit)
returns the list of clusters (list of instance indices) computed with the kmeans++ algorithm from the first operand data according to the number of clusters to split the data into (k). Usage: kmeans(data,k)

#### Special cases:     
  * if the lengths of two vectors in the right-hand aren't equal, returns 0    
  * if the lengths of two vectors in the right-hand aren't equal, returns 0

#### Examples: 
```
kmeans ([[2,4,5], [3,8,2], [1,1,3], [4,3,4]],2,10)  
list<list> var1 <- kmeans ([[2,4,5], [3,8,2], [1,1,3], [4,3,4]],2); // var1 equals []

```
  
    	
----

[//]: # (keyword|operator_kml)
### `kml`

#### Possible use: 
  *  **`kml`** (`any`) --->  `kml` 

#### Result: 
Casts the operand into the type kml
    	
----

[//]: # (keyword|operator_kurtosis)
### `kurtosis`

#### Possible use: 
  *  **`kurtosis`** (`list`) --->  `float` 

#### Result: 
returns kurtosis value computed from the operand list of values

#### Special cases:     
  * if the length of the list is lower than 3, returns NaN

#### Examples: 
```
 
float var0 <- kurtosis ([1,2,3,4,5]); // var0 equals 1.0

```
  
    	
----

[//]: # (keyword|operator_kurtosis)
### `kurtosis`

#### Possible use: 
  *  **`kurtosis`** (`container`) --->  `float`
  * `float` **`kurtosis`** `float` --->  `float`
  *  **`kurtosis`** (`float` , `float`) --->  `float` 

#### Result: 
Returns the kurtosis (aka excess) of a data sequence
Returns the kurtosis (aka excess) of a data sequence
    	
----

[//]: # (keyword|operator_last)
### `last`

#### Possible use: 
  *  **`last`** (`string`) --->  `string`
  *  **`last`** (`container<KeyType,ValueType>`) --->  `ValueType`
  * `int` **`last`** `container` --->  `list`
  *  **`last`** (`int` , `container`) --->  `list` 

#### Result: 
the last element of the operand  

#### Comment: 
the last operator behavior depends on the nature of the operand

#### Special cases:     
  * if it is a map, last returns the value of the last pair (in insertion order)    
  * if it is a file, last returns the last element of the content of the file (that is also a container)    
  * if it is a population, last returns the last agent of the population    
  * if it is a graph, last returns a list containing the last edge created    
  * if it is a matrix, last returns the element at {length-1,length-1} in the matrix    
  * for a matrix of int or float, it will return 0 if the matrix is empty    
  * for a matrix of object or geometry, it will return nil if the matrix is empty    
  * if it is a string, last returns a string composed of its last character, or an empty string if the operand is empty 
  
```
 
string var0 <- last ('abce'); // var0 equals 'e'
``` 

    
  * if it is a list, last returns the last element of the list, or nil if the list is empty 
  
```
 
int var1 <- last ([1, 2, 3]); // var1 equals 3
``` 

    


#### See also: 

[first](operators-d-to-h#first), 
    	
----

[//]: # (keyword|operator_last_index_of)
### `last_index_of`

#### Possible use: 
  * `string` **`last_index_of`** `string` --->  `int`
  *  **`last_index_of`** (`string` , `string`) --->  `int`
  * `matrix` **`last_index_of`** `unknown` --->  `point`
  *  **`last_index_of`** (`matrix` , `unknown`) --->  `point`
  * `species` **`last_index_of`** `unknown` --->  `int`
  *  **`last_index_of`** (`species` , `unknown`) --->  `int`
  * `list` **`last_index_of`** `unknown` --->  `int`
  *  **`last_index_of`** (`list` , `unknown`) --->  `int`
  * `map` **`last_index_of`** `unknown` --->  `unknown`
  *  **`last_index_of`** (`map` , `unknown`) --->  `unknown` 

#### Result: 
the index of the last occurence of the right operand in the left operand container  

#### Comment: 
The definition of last_index_of and the type of the index depend on the container

#### Special cases:     
  * if the left operand is a species, the last index of an agent is the same as its index    
  * if both operands are strings, returns the index within the left-hand string of the rightmost occurrence of the given right-hand string 
  
```
 
int var0 <- "abcabcabc" last_index_of "ca"; // var0 equals 5
``` 

    
  * if the left operand is a matrix, last_index_of returns the index as a point 
  
```
 
point var1 <- matrix([[1,2,3],[4,5,4]]) last_index_of 4; // var1 equals {1.0,2.0}
``` 

    
  * if the left operand is a list, last_index_of returns the index as an integer 
  
```
 
int var2 <- [1,2,3,4,5,6] last_index_of 4; // var2 equals 3 
int var3 <- [4,2,3,4,5,4] last_index_of 4; // var3 equals 5
``` 

    
  * if the left operand is a map, last_index_of returns the index as an int (the key of the pair) 
  
```
 
unknown var4 <- [1::2, 3::4, 5::4] last_index_of 4; // var4 equals 5
``` 

    


#### See also: 

[at](operators-a-to-a#at), [index_of](operators-i-to-m#index_of), [last_index_of](operators-i-to-m#last_index_of), 
    	
----

[//]: # (keyword|operator_last_of)
### `last_of`
   Same signification as [last](operators-i-to-m#last)
    	
----

[//]: # (keyword|operator_last_with)
### `last_with`

#### Possible use: 
  * `container` **`last_with`** `any expression` --->  `unknown`
  *  **`last_with`** (`container` , `any expression`) --->  `unknown` 

#### Result: 
the last element of the left-hand operand that makes the right-hand operand evaluate to true.  

#### Comment: 
in the right-hand operand, the keyword each can be used to represent, in turn, each of the right-hand operand elements.

#### Special cases:     
  * if the left-hand operand is nil, last_with throws an error.    
  * If there is no element that satisfies the condition, it returns nil    
  * if the left-operand is a map, the keyword each will contain each value 
  
```
 
unknown var4 <- [1::2, 3::4, 5::6] last_with (each >= 4); // var4 equals 6 
unknown var5 <- [1::2, 3::4, 5::6].pairs last_with (each.value >= 4); // var5 equals (5::6)
``` 



#### Examples: 
```
 
unknown var0 <- [1,2,3,4,5,6,7,8] last_with (each > 3); // var0 equals 8 
unknown var2 <- g2 last_with (length(g2 out_edges_of each) = 0 ); // var2 equals node11 
unknown var3 <- (list(node) last_with (round(node(each).location.x) > 32); // var3 equals node3

```
      


#### See also: 

[group_by](operators-d-to-h#group_by), [first_with](operators-d-to-h#first_with), [where](operators-s-to-z#where), 
    	
----

[//]: # (keyword|operator_layout)
### `layout`

#### Possible use: 
  * `graph` **`layout`** `string` --->  `graph`
  *  **`layout`** (`graph` , `string`) --->  `graph`
  *  **`layout`** (`graph`, `string`, `int`) --->  `graph`
  *  **`layout`** (`graph`, `string`, `int`, `map<string,unknown>`) --->  `graph` 

#### Result: 
layouts a GAMA graph.
    	
----

[//]: # (keyword|operator_length)
### `length`

#### Possible use: 
  *  **`length`** (`container<KeyType,ValueType>`) --->  `int`
  *  **`length`** (`string`) --->  `int` 

#### Result: 
the number of elements contained in the operand  

#### Comment: 
the length operator behavior depends on the nature of the operand

#### Special cases:     
  * if it is a population, length returns number of agents of the population    
  * if it is a graph, length returns the number of vertexes or of edges (depending on the way it was created)    
  * if it is a list or a map, length returns the number of elements in the list or map 
  
```
 
int var0 <- length([12,13]); // var0 equals 2 
int var1 <- length([]); // var1 equals 0
``` 

    
  * if it is a matrix, length returns the number of cells 
  
```
 
int var2 <- length(matrix([["c11","c12","c13"],["c21","c22","c23"]])); // var2 equals 6
``` 

    
  * if it is a string, length returns the number of characters 
  
```
 
int var3 <- length ('I am an agent'); // var3 equals 13
``` 


    	
----

[//]: # (keyword|operator_lgamma)
### `lgamma`
   Same signification as [log_gamma](operators-i-to-m#log_gamma)
    	
----

[//]: # (keyword|operator_line)
### `line`

#### Possible use: 
  *  **`line`** (`container<geometry>`) --->  `geometry`
  * `container<geometry>` **`line`** `float` --->  `geometry`
  *  **`line`** (`container<geometry>` , `float`) --->  `geometry` 

#### Result: 
A polyline geometry from the given list of points.
A polyline geometry from the given list of points represented as a cylinder of radius r.

#### Special cases:     
  * if the operand is nil, returns the point geometry {0,0}    
  * if the operand is composed of a single point, returns a point geometry.    
  * if the operand is nil, returns the point geometry {0,0}    
  * if the operand is composed of a single point, returns a point geometry.    
  * if a radius is added, the given list of points represented as a cylinder of radius r 
  
```
 
geometry var1 <- polyline([{0,0}, {0,10}, {10,10}, {10,0}],0.2); // var1 equals a polyline geometry composed of the 4 points.
``` 



#### Examples: 
```
 
geometry var0 <- polyline([{0,0}, {0,10}, {10,10}, {10,0}]); // var0 equals a polyline geometry composed of the 4 points.

```
      


#### See also: 

[around](operators-a-to-a#around), [circle](operators-b-to-c#circle), [cone](operators-b-to-c#cone), [link](operators-i-to-m#link), [norm](operators-n-to-r#norm), [point](operators-n-to-r#point), [polygone](operators-s-to-z#polygone), [rectangle](operators-n-to-r#rectangle), [square](operators-s-to-z#square), [triangle](operators-s-to-z#triangle), 
    	
----

[//]: # (keyword|operator_link)
### `link`

#### Possible use: 
  * `geometry` **`link`** `geometry` --->  `geometry`
  *  **`link`** (`geometry` , `geometry`) --->  `geometry` 

#### Result: 
A dynamic line geometry between the location of the two operands  

#### Comment: 
The geometry of the link is a line between the locations of the two operands, which is built and maintained dynamically

#### Special cases:     
  * if one of the operands is nil, link returns a point geometry at the location of the other. If both are null, it returns a point geometry at {0,0}

#### Examples: 
```
 
geometry var0 <- link (geom1,geom2); // var0 equals a link geometry between geom1 and geom2.

```
      


#### See also: 

[around](operators-a-to-a#around), [circle](operators-b-to-c#circle), [cone](operators-b-to-c#cone), [line](operators-i-to-m#line), [norm](operators-n-to-r#norm), [point](operators-n-to-r#point), [polygon](operators-n-to-r#polygon), [polyline](operators-n-to-r#polyline), [rectangle](operators-n-to-r#rectangle), [square](operators-s-to-z#square), [triangle](operators-s-to-z#triangle), 
    	
----

[//]: # (keyword|operator_list)
### `list`

#### Possible use: 
  *  **`list`** (`any`) --->  `list` 

#### Result: 
Casts the operand into the type list
    	
----

[//]: # (keyword|operator_list_with)
### `list_with`

#### Possible use: 
  * `int` **`list_with`** `any expression` --->  `list`
  *  **`list_with`** (`int` , `any expression`) --->  `list` 

#### Result: 
creates a list with a size provided by the first operand, and filled with the second operand  

#### Comment: 
Note that the right operand  should be positive, and that the second one is evaluated for each position  in the list.    


#### See also: 

[list](operators-i-to-m#list), 
    	
----

[//]: # (keyword|operator_ln)
### `ln`

#### Possible use: 
  *  **`ln`** (`float`) --->  `float`
  *  **`ln`** (`int`) --->  `float` 

#### Result: 
Returns the natural logarithm (base e) of the operand.

#### Special cases:     
  * an exception is raised if the operand is less than zero.

#### Examples: 
```
 
float var0 <- ln(exp(1)); // var0 equals 1.0 
float var1 <- ln(1); // var1 equals 0.0

```
      


#### See also: 

[exp](operators-d-to-h#exp), 
    	
----

[//]: # (keyword|operator_load_graph_from_file)
### `load_graph_from_file`

#### Possible use: 
  *  **`load_graph_from_file`** (`string`) --->  `graph`
  * `string` **`load_graph_from_file`** `string` --->  `graph`
  *  **`load_graph_from_file`** (`string` , `string`) --->  `graph`
  * `string` **`load_graph_from_file`** `file` --->  `graph`
  *  **`load_graph_from_file`** (`string` , `file`) --->  `graph`
  *  **`load_graph_from_file`** (`string`, `species`, `species`) --->  `graph`
  *  **`load_graph_from_file`** (`string`, `string`, `species`, `species`) --->  `graph`
  *  **`load_graph_from_file`** (`string`, `file`, `species`, `species`) --->  `graph`
  *  **`load_graph_from_file`** (`string`, `string`, `species`, `species`, `bool`) --->  `graph` 

#### Result: 
loads a graph from a file
returns a graph loaded from a given file encoded into a given format. The last boolean parameter indicates whether the resulting graph will be considered as spatial or not by GAMA  

#### Comment: 
Available formats: "pajek": Pajek (Slovene word for Spider) is a program, for Windows, for analysis and visualization of large networks. See: http://pajek.imfm.si/doku.php?id=pajek for more details."lgl": LGL is a compendium of applications for making the visualization of large networks and trees tractable. See: http://lgl.sourceforge.net/ for more details."dot": DOT is a plain text graph description language. It is a simple way of describing graphs that both humans and computer programs can use. See: http://en.wikipedia.org/wiki/DOT_language for more details."edge": This format is a simple text file with numeric vertex ids defining the edges."gexf": GEXF (Graph Exchange XML Format) is a language for describing complex networks structures, their associated data and dynamics. Started in 2007 at Gephi project by different actors, deeply involved in graph exchange issues, the gexf specifications are mature enough to claim being both extensible and open, and suitable for real specific applications. See: http://gexf.net/format/ for more details."graphml": GraphML is a comprehensive and easy-to-use file format for graphs based on XML. See: http://graphml.graphdrawing.org/ for more details."tlp" or "tulip": TLP is the Tulip software graph format. See: http://tulip.labri.fr/TulipDrupal/?q=tlp-file-format for more details. "ncol": This format is used by the Large Graph Layout progra. It is simply a symbolic weighted edge list. It is a simple text file with one edge per line. An edge is defined by two symbolic vertex names separated by whitespace. (The symbolic vertex names themselves cannot contain whitespace.) They might followed by an optional number, this will be the weight of the edge. See: http://bioinformatics.icmb.utexas.edu/lgl for more details.The map operand should includes following elements:Available formats: "pajek": Pajek (Slovene word for Spider) is a program, for Windows, for analysis and visualization of large networks. See: http://pajek.imfm.si/doku.php?id=pajek for more details."lgl": LGL is a compendium of applications for making the visualization of large networks and trees tractable. See: http://lgl.sourceforge.net/ for more details."dot": DOT is a plain text graph description language. It is a simple way of describing graphs that both humans and computer programs can use. See: http://en.wikipedia.org/wiki/DOT_language for more details."edge": This format is a simple text file with numeric vertex ids defining the edges."gexf": GEXF (Graph Exchange XML Format) is a language for describing complex networks structures, their associated data and dynamics. Started in 2007 at Gephi project by different actors, deeply involved in graph exchange issues, the gexf specifications are mature enough to claim being both extensible and open, and suitable for real specific applications. See: http://gexf.net/format/ for more details."graphml": GraphML is a comprehensive and easy-to-use file format for graphs based on XML. See: http://graphml.graphdrawing.org/ for more details."tlp" or "tulip": TLP is the Tulip software graph format. See: http://tulip.labri.fr/TulipDrupal/?q=tlp-file-format for more details. "ncol": This format is used by the Large Graph Layout progra. It is simply a symbolic weighted edge list. It is a simple text file with one edge per line. An edge is defined by two symbolic vertex names separated by whitespace. (The symbolic vertex names themselves cannot contain whitespace.) They might followed by an optional number, this will be the weight of the edge. See: http://bioinformatics.icmb.utexas.edu/lgl for more details.The map operand should includes following elements:

#### Special cases:     
  * "format": the format of the file    
  * "filename": the filename of the file containing the network    
  * "edges_species": the species of edges    
  * "vertices_specy": the species of vertices    
  * "format": the format of the file    
  * "filename": the filename of the file containing the network    
  * "edges_species": the species of edges    
  * "vertices_specy": the species of vertices    
  * "filename": the filename of the file containing the network, "edges_species": the species of edges, "vertices_specy": the species of vertices 
  
```
graph<myVertexSpecy,myEdgeSpecy> myGraph <- load_graph_from_file( 			"pajek", 			"./example_of_Pajek_file", 			myVertexSpecy, 			myEdgeSpecy ); 
``` 

    
  * "file": the file containing the network 
  
```
graph<myVertexSpecy,myEdgeSpecy> myGraph <- load_graph_from_file( 			"pajek", 			"example_of_Pajek_file"); 
``` 

    
  * "format": the format of the file, "filename": the filename of the file containing the network 
  
```
graph<myVertexSpecy,myEdgeSpecy> myGraph <- load_graph_from_file( 			"pajek", 			"example_of_Pajek_file"); 
``` 

    
  * "format": the format of the file, "file": the file containing the network 
  
```
graph<myVertexSpecy,myEdgeSpecy> myGraph <- load_graph_from_file( 			"pajek", 			"example_of_Pajek_file"); 
``` 

    
  * "format": the format of the file, "file": the file containing the network, "edges_species": the species of edges, "vertices_specy": the species of vertices 
  
```
graph<myVertexSpecy,myEdgeSpecy> myGraph <- load_graph_from_file( 			"pajek", 			"example_of_Pajek_file", 			myVertexSpecy, 			myEdgeSpecy ); 
``` 



#### Examples: 
```
graph<myVertexSpecy,myEdgeSpecy> myGraph <- load_graph_from_file( 			"pajek", 			"./example_of_Pajek_file", 			myVertexSpecy, 			myEdgeSpecy); graph<myVertexSpecy,myEdgeSpecy> myGraph <- load_graph_from_file( 			"pajek", 			"./example_of_Pajek_file", 			myVertexSpecy, 			myEdgeSpecy , true); 

```
  
    	
----

[//]: # (keyword|operator_load_shortest_paths)
### `load_shortest_paths`

#### Possible use: 
  * `graph` **`load_shortest_paths`** `matrix` --->  `graph`
  *  **`load_shortest_paths`** (`graph` , `matrix`) --->  `graph` 

#### Result: 
put in the graph cache the computed shortest paths contained in the matrix (rows: source, columns: target)

#### Examples: 
```
 
graph var0 <- load_shortest_paths(shortest_paths_matrix); // var0 equals return my_graph with all the shortest paths computed

```
  
    	
----

[//]: # (keyword|operator_load_sub_model)
### `load_sub_model`

#### Possible use: 
  * `string` **`load_sub_model`** `string` --->  `msi.gama.kernel.experiment.IExperimentAgent`
  *  **`load_sub_model`** (`string` , `string`) --->  `msi.gama.kernel.experiment.IExperimentAgent` 

#### Result: 
Load a submodel  

#### Comment: 
loaded submodel
    	
----

[//]: # (keyword|operator_log)
### `log`

#### Possible use: 
  *  **`log`** (`int`) --->  `float`
  *  **`log`** (`float`) --->  `float` 

#### Result: 
Returns the logarithm (base 10) of the operand.

#### Special cases:     
  * an exception is raised if the operand is equals or less than zero.

#### Examples: 
```
 
float var0 <- log(1); // var0 equals 0.0 
float var1 <- log(10); // var1 equals 1.0

```
      


#### See also: 

[ln](operators-i-to-m#ln), 
    	
----

[//]: # (keyword|operator_log_gamma)
### `log_gamma`

#### Possible use: 
  *  **`log_gamma`** (`float`) --->  `float` 

#### Result: 
Returns the log of the value of the Gamma function at x.
    	
----

[//]: # (keyword|operator_lower_case)
### `lower_case`

#### Possible use: 
  *  **`lower_case`** (`string`) --->  `string` 

#### Result: 
Converts all of the characters in the string operand to lower case

#### Examples: 
```
 
string var0 <- lower_case("Abc"); // var0 equals 'abc'

```
      


#### See also: 

[upper_case](operators-s-to-z#upper_case), 
    	
----

[//]: # (keyword|operator_main_connected_component)
### `main_connected_component`

#### Possible use: 
  *  **`main_connected_component`** (`graph`) --->  `graph` 

#### Result: 
returns the sub-graph corresponding to the main connected components of the graph

#### Examples: 
```
 
graph var0 <- main_connected_component(my_graph); // var0 equals the sub-graph corresponding to the main connected components of the graph

```
      


#### See also: 

[connected_components_of](operators-b-to-c#connected_components_of), 
    	
----

[//]: # (keyword|operator_map)
### `map`

#### Possible use: 
  *  **`map`** (`any`) --->  `map` 

#### Result: 
Casts the operand into the type map
    	
----

[//]: # (keyword|operator_masked_by)
### `masked_by`

#### Possible use: 
  * `geometry` **`masked_by`** `container<geometry>` --->  `geometry`
  *  **`masked_by`** (`geometry` , `container<geometry>`) --->  `geometry`
  *  **`masked_by`** (`geometry`, `container<geometry>`, `int`) --->  `geometry`

#### Examples: 
```
 
geometry var0 <- perception_geom masked_by obstacle_list; // var0 equals the geometry representing the part of perception_geom visible from the agent position considering the list of obstacles obstacle_list. 
geometry var1 <- perception_geom masked_by obstacle_list; // var1 equals the geometry representing the part of perception_geom visible from the agent position considering the list of obstacles obstacle_list.

```
  
    	
----

[//]: # (keyword|operator_material)
### `material`

#### Possible use: 
  * `float` **`material`** `float` --->  `msi.gama.util.GamaMaterial`
  *  **`material`** (`float` , `float`) --->  `msi.gama.util.GamaMaterial` 

#### Result: 
Returns

#### Examples: 
```
 

```
      


#### See also: 

[](operators-s-to-z#), 
    	
----

[//]: # (keyword|operator_material)
### `material`

#### Possible use: 
  *  **`material`** (`any`) --->  `material` 

#### Result: 
Casts the operand into the type material
    	
----

[//]: # (keyword|operator_matrix)
### `matrix`

#### Possible use: 
  *  **`matrix`** (`any`) --->  `matrix` 

#### Result: 
Casts the operand into the type matrix
    	
----

[//]: # (keyword|operator_matrix_with)
### `matrix_with`

#### Possible use: 
  * `point` **`matrix_with`** `any expression` --->  `matrix`
  *  **`matrix_with`** (`point` , `any expression`) --->  `matrix` 

#### Result: 
creates a matrix with a size provided by the first operand, and filled with the second operand  

#### Comment: 
Note that both components of the right operand point should be positive, otherwise an exception is raised.    


#### See also: 

[matrix](operators-i-to-m#matrix), [as_matrix](operators-a-to-a#as_matrix), 
    	
----

[//]: # (keyword|operator_max)
### `max`

#### Possible use: 
  *  **`max`** (`container`) --->  `unknown` 

#### Result: 
the maximum element found in the operand  

#### Comment: 
the max operator behavior depends on the nature of the operand

#### Special cases:     
  * if it is a population of a list of other type: max transforms all elements into integer and returns the maximum of them    
  * if it is a map, max returns the maximum among the list of all elements value    
  * if it is a file, max returns the maximum of the content of the file (that is also a container)    
  * if it is a graph, max returns the maximum of the list of the elements of the graph (that can be the list of edges or vertexes depending on the graph)    
  * if it is a matrix of int, float or object, max returns the maximum of all the numerical elements (thus all elements for integer and float matrices)    
  * if it is a matrix of geometry, max returns the maximum of the list of the geometries    
  * if it is a matrix of another type, max returns the maximum of the elements transformed into float    
  * if it is a list of int of float, max returns the maximum of all the elements 
  
```
 
unknown var0 <- max ([100, 23.2, 34.5]); // var0 equals 100.0
``` 

    
  * if it is a list of points: max returns the maximum of all points as a point (i.e. the point with the greatest coordinate on the x-axis, in case of equality the point with the greatest coordinate on the y-axis is chosen. If all the points are equal, the first one is returned. ) 
  
```
 
unknown var1 <- max([{1.0,3.0},{3.0,5.0},{9.0,1.0},{7.0,8.0}]); // var1 equals {9.0,1.0}
``` 

    


#### See also: 

[min](operators-i-to-m#min), 
    	
----

[//]: # (keyword|operator_max_flow_between)
### `max_flow_between`

#### Possible use: 
  *  **`max_flow_between`** (`graph`, `unknown`, `unknown`) --->  `msi.gama.util.GamaMap<java.lang.Object,java.lang.Double>` 

#### Result: 
The max flow (map<edge,flow> in a graph between the source and the sink using Edmonds-Karp algorithm

#### Examples: 
```
max_flow_between(my_graph, vertice1, vertice2) 

```
  
    	
----

[//]: # (keyword|operator_max_of)
### `max_of`

#### Possible use: 
  * `container` **`max_of`** `any expression` --->  `unknown`
  *  **`max_of`** (`container` , `any expression`) --->  `unknown` 

#### Result: 
the maximum value of the right-hand expression evaluated on each of the elements of the left-hand operand  

#### Comment: 
in the right-hand operand, the keyword each can be used to represent, in turn, each of the right-hand operand elements.

#### Special cases:     
  * As of GAMA 1.6, if the left-hand operand is nil or empty, max_of throws an error    
  * if the left-operand is a map, the keyword each will contain each value 
  
```
 
unknown var4 <- [1::2, 3::4, 5::6] max_of (each + 3); // var4 equals 9
``` 



#### Examples: 
```
 
unknown var0 <- [1,2,4,3,5,7,6,8] max_of (each * 100 ); // var0 equals 800graph g2 <- as_edge_graph([{1,5}::{12,45},{12,45}::{34,56}]);  
unknown var2 <- g2.vertices max_of (g2 degree_of( each )); // var2 equals 2 
unknown var3 <- (list(node) max_of (round(node(each).location.x)); // var3 equals 96

```
      


#### See also: 

[min_of](operators-i-to-m#min_of), 
    	
----

[//]: # (keyword|operator_maximal_cliques_of)
### `maximal_cliques_of`

#### Possible use: 
  *  **`maximal_cliques_of`** (`graph`) --->  `list<list>` 

#### Result: 
returns the maximal cliques of a graph using the Bron-Kerbosch clique detection algorithm: A clique is maximal if it is impossible to enlarge it by adding another vertex from the graph. Note that a maximal clique is not necessarily the biggest clique in the graph.

#### Examples: 
```
graph my_graph <- graph([]);  
list<list> var1 <- maximal_cliques_of (my_graph); // var1 equals the list of all the maximal cliques as list

```
      


#### See also: 

[biggest_cliques_of](operators-b-to-c#biggest_cliques_of), 
    	
----

[//]: # (keyword|operator_mean)
### `mean`

#### Possible use: 
  *  **`mean`** (`container`) --->  `unknown` 

#### Result: 
the mean of all the elements of the operand  

#### Comment: 
the elements of the operand are summed (see sum for more details about the sum of container elements ) and then the sum value is divided by the number of elements.

#### Special cases:     
  * if the container contains points, the result will be a point. If the container contains rgb values, the result will be a rgb color

#### Examples: 
```
 
unknown var0 <- mean ([4.5, 3.5, 5.5, 7.0]); // var0 equals 5.125 

```
      


#### See also: 

[sum](operators-s-to-z#sum), 
    	
----

[//]: # (keyword|operator_mean_deviation)
### `mean_deviation`

#### Possible use: 
  *  **`mean_deviation`** (`container`) --->  `float` 

#### Result: 
the deviation from the mean of all the elements of the operand. See <A href= "http://en.wikipedia.org/wiki/Absolute_deviation" >Mean_deviation</A> for more details.  

#### Comment: 
The operator casts all the numerical element of the list into float. The elements that are not numerical are discarded.

#### Examples: 
```
 
float var0 <- mean_deviation ([4.5, 3.5, 5.5, 7.0]); // var0 equals 1.125

```
      


#### See also: 

[mean](operators-i-to-m#mean), [standard_deviation](operators-s-to-z#standard_deviation), 
    	
----

[//]: # (keyword|operator_mean_of)
### `mean_of`

#### Possible use: 
  * `container` **`mean_of`** `any expression` --->  `unknown`
  *  **`mean_of`** (`container` , `any expression`) --->  `unknown` 

#### Result: 
the mean of the right-hand expression evaluated on each of the elements of the left-hand operand  

#### Comment: 
in the right-hand operand, the keyword each can be used to represent, in turn, each of the right-hand operand elements.

#### Special cases:     
  * if the left-operand is a map, the keyword each will contain each value 
  
```
 
unknown var1 <- [1::2, 3::4, 5::6] mean_of (each); // var1 equals 4
``` 



#### Examples: 
```
 
unknown var0 <- [1,2] mean_of (each * 10 ); // var0 equals 15

```
      


#### See also: 

[min_of](operators-i-to-m#min_of), [max_of](operators-i-to-m#max_of), [sum_of](operators-s-to-z#sum_of), [product_of](operators-n-to-r#product_of), 
    	
----

[//]: # (keyword|operator_meanR)
### `meanR`

#### Possible use: 
  *  **`meanR`** (`container`) --->  `unknown` 

#### Result: 
returns the mean value of given vector (right-hand operand) in given variable  (left-hand operand).

#### Examples: 
```
list<int> X <- [2, 3, 1];  
int var1 <- meanR(X); // var1 equals 2

```
  
    	
----

[//]: # (keyword|operator_median)
### `median`

#### Possible use: 
  *  **`median`** (`container`) --->  `unknown` 

#### Result: 
the median of all the elements of the operand.

#### Special cases:     
  * if the container contains points, the result will be a point. If the container contains rgb values, the result will be a rgb color

#### Examples: 
```
 
unknown var0 <- median ([4.5, 3.5, 5.5, 3.4, 7.0]); // var0 equals 4.5

```
      


#### See also: 

[mean](operators-i-to-m#mean), 
    	
----

[//]: # (keyword|operator_mental_state)
### `mental_state`

#### Possible use: 
  *  **`mental_state`** (`any`) --->  `mental_state` 

#### Result: 
Casts the operand into the type mental_state
    	
----

[//]: # (keyword|operator_message)
### `message`

#### Possible use: 
  *  **`message`** (`unknown`) --->  `msi.gama.extensions.messaging.GamaMessage` 

#### Result: 
to be added
    	
----

[//]: # (keyword|operator_milliseconds_between)
### `milliseconds_between`

#### Possible use: 
  * `date` **`milliseconds_between`** `date` --->  `float`
  *  **`milliseconds_between`** (`date` , `date`) --->  `float` 

#### Result: 
Provide the exact number of milliseconds between two dates. This number can be positive or negative (if the second operand is smaller than the first one)

#### Examples: 
```
 
float var0 <- milliseconds_between(date('2000-01-01'), date('2000-02-01')); // var0 equals 2.6784E9

```
  
    	
----

[//]: # (keyword|operator_min)
### `min`

#### Possible use: 
  *  **`min`** (`container`) --->  `unknown` 

#### Result: 
the minimum element found in the operand.  

#### Comment: 
the min operator behavior depends on the nature of the operand

#### Special cases:     
  * if it is a list of points: min returns the minimum of all points as a point (i.e. the point with the smallest coordinate on the x-axis, in case of equality the point with the smallest coordinate on the y-axis is chosen. If all the points are equal, the first one is returned. )    
  * if it is a population of a list of other types: min transforms all elements into integer and returns the minimum of them    
  * if it is a map, min returns the minimum among the list of all elements value    
  * if it is a file, min returns the minimum of the content of the file (that is also a container)    
  * if it is a graph, min returns the minimum of the list of the elements of the graph (that can be the list of edges or vertexes depending on the graph)    
  * if it is a matrix of int, float or object, min returns the minimum of all the numerical elements (thus all elements for integer and float matrices)    
  * if it is a matrix of geometry, min returns the minimum of the list of the geometries    
  * if it is a matrix of another type, min returns the minimum of the elements transformed into float    
  * if it is a list of int or float: min returns the minimum of all the elements 
  
```
 
unknown var0 <- min ([100, 23.2, 34.5]); // var0 equals 23.2
``` 

    


#### See also: 

[max](operators-i-to-m#max), 
    	
----

[//]: # (keyword|operator_min_of)
### `min_of`

#### Possible use: 
  * `container` **`min_of`** `any expression` --->  `unknown`
  *  **`min_of`** (`container` , `any expression`) --->  `unknown` 

#### Result: 
the minimum value of the right-hand expression evaluated on each of the elements of the left-hand operand  

#### Comment: 
in the right-hand operand, the keyword each can be used to represent, in turn, each of the right-hand operand elements.

#### Special cases:     
  * if the left-hand operand is nil or empty, min_of throws an error    
  * if the left-operand is a map, the keyword each will contain each value 
  
```
 
unknown var4 <- [1::2, 3::4, 5::6] min_of (each + 3); // var4 equals 5
``` 



#### Examples: 
```
 
unknown var0 <- [1,2,4,3,5,7,6,8] min_of (each * 100 ); // var0 equals 100graph g2 <- as_edge_graph([{1,5}::{12,45},{12,45}::{34,56}]);  
unknown var2 <- g2 min_of (length(g2 out_edges_of each) ); // var2 equals 0 
unknown var3 <- (list(node) min_of (round(node(each).location.x)); // var3 equals 4

```
      


#### See also: 

[max_of](operators-i-to-m#max_of), 
    	
----

[//]: # (keyword|operator_minus_days)
### `minus_days`

#### Possible use: 
  * `date` **`minus_days`** `int` --->  `date`
  *  **`minus_days`** (`date` , `int`) --->  `date` 

#### Result: 
Subtract a given number of days from a date

#### Examples: 
```
 
date var0 <- date('2000-01-01') minus_days 20; // var0 equals date('1999-12-12')

```
  
    	
----

[//]: # (keyword|operator_minus_hours)
### `minus_hours`

#### Possible use: 
  * `date` **`minus_hours`** `int` --->  `date`
  *  **`minus_hours`** (`date` , `int`) --->  `date` 

#### Result: 
Remove a given number of hours from a date

#### Examples: 
```
// equivalent to date1 - 15 #h  
date var1 <- date('2000-01-01') minus_hours 15 ; // var1 equals date('1999-12-31 09:00:00')

```
  
    	
----

[//]: # (keyword|operator_minus_minutes)
### `minus_minutes`

#### Possible use: 
  * `date` **`minus_minutes`** `int` --->  `date`
  *  **`minus_minutes`** (`date` , `int`) --->  `date` 

#### Result: 
Subtract a given number of minutes from a date

#### Examples: 
```
// date('2000-01-01') to date1 - 5#mn  
date var1 <- date('2000-01-01') minus_minutes 5 ; // var1 equals date('1999-12-31 23:55:00')

```
  
    	
----

[//]: # (keyword|operator_minus_months)
### `minus_months`

#### Possible use: 
  * `date` **`minus_months`** `int` --->  `date`
  *  **`minus_months`** (`date` , `int`) --->  `date` 

#### Result: 
Subtract a given number of months from a date

#### Examples: 
```
 
date var0 <- date('2000-01-01') minus_months 5; // var0 equals date('1999-08-01')

```
  
    	
----

[//]: # (keyword|operator_minus_ms)
### `minus_ms`

#### Possible use: 
  * `date` **`minus_ms`** `int` --->  `date`
  *  **`minus_ms`** (`date` , `int`) --->  `date` 

#### Result: 
Remove a given number of milliseconds from a date

#### Examples: 
```
// equivalent to date1 - 15 #ms  
date var1 <- date('2000-01-01') minus_ms 1000 ; // var1 equals date('1999-12-31 23:59:59')

```
  
    	
----

[//]: # (keyword|operator_minus_seconds)
### `minus_seconds`
   Same signification as [-](operators-a-to-a#-)
    	
----

[//]: # (keyword|operator_minus_weeks)
### `minus_weeks`

#### Possible use: 
  * `date` **`minus_weeks`** `int` --->  `date`
  *  **`minus_weeks`** (`date` , `int`) --->  `date` 

#### Result: 
Subtract a given number of weeks from a date

#### Examples: 
```
 
date var0 <- date('2000-01-01') minus_weeks 15; // var0 equals date('1999-09-18')

```
  
    	
----

[//]: # (keyword|operator_minus_years)
### `minus_years`

#### Possible use: 
  * `date` **`minus_years`** `int` --->  `date`
  *  **`minus_years`** (`date` , `int`) --->  `date` 

#### Result: 
Subtract a given number of year from a date

#### Examples: 
```
 
date var0 <- date('2000-01-01') minus_years 3; // var0 equals date('1997-01-01')

```
  
    	
----

[//]: # (keyword|operator_mod)
### `mod`

#### Possible use: 
  * `int` **`mod`** `int` --->  `int`
  *  **`mod`** (`int` , `int`) --->  `int` 

#### Result: 
Returns the remainder of the integer division of the left-hand operand by the right-hand operand.

#### Special cases:     
  * if operands are float, they are truncated    
  * if the right-hand operand is equal to zero, raises an exception.

#### Examples: 
```
 
int var0 <- 40 mod 3; // var0 equals 1

```
      


#### See also: 

[div](operators-d-to-h#div), 
    	
----

[//]: # (keyword|operator_moment)
### `moment`

#### Possible use: 
  *  **`moment`** (`container`, `int`, `float`) --->  `float` 

#### Result: 
Returns the moment of k-th order with constant c of a data sequence
    	
----

[//]: # (keyword|operator_months_between)
### `months_between`

#### Possible use: 
  * `date` **`months_between`** `date` --->  `int`
  *  **`months_between`** (`date` , `date`) --->  `int` 

#### Result: 
Provide the exact number of months between two dates. This number can be positive or negative (if the second operand is smaller than the first one)

#### Examples: 
```
 
int var0 <- months_between(date('2000-01-01'), date('2000-02-01')); // var0 equals 1

```
  
    	
----

[//]: # (keyword|operator_moran)
### `moran`

#### Possible use: 
  * `list<float>` **`moran`** `matrix<float>` --->  `float`
  *  **`moran`** (`list<float>` , `matrix<float>`) --->  `float`

#### Special cases:     
  * return the Moran Index of the given list of interest points (list of floats) and the weight matrix (matrix of float) 
  
```
 
float var0 <- moran([1.0, 0.5, 2.0], weight_matrix); // var0 equals the Moran index computed
``` 


    	
----

[//]: # (keyword|operator_mul)
### `mul`

#### Possible use: 
  *  **`mul`** (`container`) --->  `unknown` 

#### Result: 
the product of all the elements of the operand  

#### Comment: 
the mul operator behavior depends on the nature of the operand

#### Special cases:     
  * if it is a list of points: mul returns the product of all points as a point (each coordinate is the product of the corresponding coordinate of each element)    
  * if it is a list of other types: mul transforms all elements into integer and multiplies them    
  * if it is a map, mul returns the product of the value of all elements    
  * if it is a file, mul returns the product of the content of the file (that is also a container)    
  * if it is a graph, mul returns the product of the list of the elements of the graph (that can be the list of edges or vertexes depending on the graph)    
  * if it is a matrix of int, float or object, mul returns the product of all the numerical elements (thus all elements for integer and float matrices)    
  * if it is a matrix of geometry, mul returns the product of the list of the geometries    
  * if it is a matrix of other types: mul transforms all elements into float and multiplies them    
  * if it is a list of int or float: mul returns the product of all the elements 
  
```
 
unknown var0 <- mul ([100, 23.2, 34.5]); // var0 equals 80040.0
``` 

    


#### See also: 

[sum](operators-s-to-z#sum), 