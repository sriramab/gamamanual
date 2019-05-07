# Operators (B to C)
 	

	
    	
----

[//]: # (keyword|operator_BDIPlan)
### `BDIPlan`

#### Possible use: 
  *  **`BDIPlan`** (`any`) --->  `BDIPlan` 

#### Result: 
Casts the operand into the type BDIPlan
    	
----

[//]: # (keyword|operator_before)
### `before`

#### Possible use: 
  *  **`before`** (`date`) --->  `bool`
  * `any expression` **`before`** `date` --->  `bool`
  *  **`before`** (`any expression` , `date`) --->  `bool` 

#### Result: 
Returns true if the current_date of the model is strictly before the date passed in argument. Synonym of 'current_date < argument'

#### Examples: 
```
reflex when: before(starting_date) {} 	// this reflex will never be run 

```
  
    	
----

[//]: # (keyword|operator_beta)
### `beta`

#### Possible use: 
  * `float` **`beta`** `float` --->  `float`
  *  **`beta`** (`float` , `float`) --->  `float` 

#### Result: 
Returns the beta function with arguments a, b.
    	
----

[//]: # (keyword|operator_beta_index)
### `beta_index`

#### Possible use: 
  *  **`beta_index`** (`graph`) --->  `float` 

#### Result: 
returns the beta index of the graph (Measures the level of connectivity in a graph and is expressed by the relationship between the number of links (e) over the number of nodes (v) : beta = e/v.

#### Examples: 
```
graph graphEpidemio <- graph([]);  
float var1 <- beta_index(graphEpidemio); // var1 equals the beta index of the graph

```
      


#### See also: 

[alpha_index](operators-a-to-a#alpha_index), [gamma_index](operators-d-to-h#gamma_index), [nb_cycles](operators-n-to-r#nb_cycles), [connectivity_index](operators-b-to-c#connectivity_index), 
    	
----

[//]: # (keyword|operator_between)
### `between`

#### Possible use: 
  * `date` **`between`** `date` --->  `bool`
  *  **`between`** (`date` , `date`) --->  `bool`
  *  **`between`** (`any expression`, `date`, `date`) --->  `bool`
  *  **`between`** (`int`, `int`, `int`) --->  `bool`
  *  **`between`** (`date`, `date`, `date`) --->  `bool`
  *  **`between`** (`float`, `float`, `float`) --->  `bool` 

#### Result: 
returns true the first integer operand is bigger than the second integer operand and smaller than the third integer operand

returns true if the first float operand is bigger than the second float operand and smaller than the third float operand

#### Special cases:     
  * returns true if the first operand is between the two dates passed in arguments (both exclusive). The version with 2 arguments compares the current_date with the 2 others 
  
```
 
bool var0 <- (date('2016-01-01') between(date('2000-01-01'), date('2020-02-02'))); // var0 equals true// // will return true if the current_date of the model is in_between the 2 between(date('2000-01-01'), date('2020-02-02')) 
``` 

    
  * returns true if the first operand is between the two dates passed in arguments (both exclusive). Can be combined with 'every' to express a frequency between two dates 
  
```
 
bool var3 <- (date('2016-01-01') between(date('2000-01-01'), date('2020-02-02'))); // var3 equals true// will return true every new day between these two dates, taking the first one as the starting point every(#day between(date('2000-01-01'), date('2020-02-02')))  
``` 



#### Examples: 
```
 
bool var6 <- between(5, 1, 10); // var6 equals true 
bool var7 <- between(5.0, 1.0, 10.0); // var7 equals true

```
  
    	
----

[//]: # (keyword|operator_betweenness_centrality)
### `betweenness_centrality`

#### Possible use: 
  *  **`betweenness_centrality`** (`graph`) --->  `map` 

#### Result: 
returns a map containing for each vertex (key), its betweenness centrality (value): number of shortest paths passing through each vertex

#### Examples: 
```
graph graphEpidemio <- graph([]);  
map var1 <- betweenness_centrality(graphEpidemio); // var1 equals the betweenness centrality index of the graph

```
  
    	
----

[//]: # (keyword|operator_biggest_cliques_of)
### `biggest_cliques_of`

#### Possible use: 
  *  **`biggest_cliques_of`** (`graph`) --->  `list<list>` 

#### Result: 
returns the biggest cliques of a graph using the Bron-Kerbosch clique detection algorithm

#### Examples: 
```
graph my_graph <- graph([]);  
list<list> var1 <- biggest_cliques_of (my_graph); // var1 equals the list of the biggest cliques as list

```
      


#### See also: 

[maximal_cliques_of](operators-i-to-m#maximal_cliques_of), 
    	
----

[//]: # (keyword|operator_binomial)
### `binomial`

#### Possible use: 
  * `int` **`binomial`** `float` --->  `int`
  *  **`binomial`** (`int` , `float`) --->  `int` 

#### Result: 
A value from a random variable following a binomial distribution. The operands represent the number of experiments n and the success probability p.  

#### Comment: 
The binomial distribution is the discrete probability distribution of the number of successes in a sequence of n independent yes/no experiments, each of which yields success with probability p, cf. Binomial distribution on Wikipedia.

#### Examples: 
```
 
int var0 <- binomial(15,0.6); // var0 equals a random positive integer

```
      


#### See also: 

[poisson](operators-n-to-r#poisson), [gauss](operators-d-to-h#gauss), 
    	
----

[//]: # (keyword|operator_binomial_coeff)
### `binomial_coeff`

#### Possible use: 
  * `int` **`binomial_coeff`** `int` --->  `float`
  *  **`binomial_coeff`** (`int` , `int`) --->  `float` 

#### Result: 
Returns n choose k as a double. Note the integerization of the double return value.
    	
----

[//]: # (keyword|operator_binomial_complemented)
### `binomial_complemented`

#### Possible use: 
  *  **`binomial_complemented`** (`int`, `int`, `float`) --->  `float` 

#### Result: 
Returns the sum of the terms k+1 through n of the Binomial probability density, where n is the number of trials and P is the probability of success in the range 0 to 1.
    	
----

[//]: # (keyword|operator_binomial_sum)
### `binomial_sum`

#### Possible use: 
  *  **`binomial_sum`** (`int`, `int`, `float`) --->  `float` 

#### Result: 
Returns the sum of the terms 0 through k of the Binomial probability density, where n is the number of trials and p is the probability of success in the range 0 to 1.
    	
----

[//]: # (keyword|operator_blend)
### `blend`

#### Possible use: 
  * `rgb` **`blend`** `rgb` --->  `rgb`
  *  **`blend`** (`rgb` , `rgb`) --->  `rgb`
  *  **`blend`** (`rgb`, `rgb`, `float`) --->  `rgb` 

#### Result: 
Blend two colors with an optional ratio (c1 `*` r + c2 `*` (1 - r)) between 0 and 1

#### Special cases:     
  * If the ratio is omitted, an even blend is done 
  
```
 
rgb var1 <- blend(#red, #blue); // var1 equals to a color very close to the purple
``` 



#### Examples: 
```
 
rgb var3 <- blend(#red, #blue, 0.3); // var3 equals to a color between the purple and the blue

```
      


#### See also: 

[rgb](operators-n-to-r#rgb), [hsb](operators-d-to-h#hsb), 
    	
----

[//]: # (keyword|operator_bool)
### `bool`

#### Possible use: 
  *  **`bool`** (`any`) --->  `bool` 

#### Result: 
Casts the operand into the type bool
    	
----

[//]: # (keyword|operator_box)
### `box`

#### Possible use: 
  *  **`box`** (`point`) --->  `geometry`
  *  **`box`** (`float`, `float`, `float`) --->  `geometry` 

#### Result: 
A box geometry which side sizes are given by the operands.  

#### Comment: 
the center of the box is by default the location of the current agent in which has been called this operator.the center of the box is by default the location of the current agent in which has been called this operator.

#### Special cases:     
  * returns nil if the operand is nil.    
  * returns nil if the operand is nil.

#### Examples: 
```
 
geometry var0 <- box(10, 5 , 5); // var0 equals a geometry as a rectangle with width = 10, height = 5 depth= 5. 
geometry var1 <- box({10, 5 , 5}); // var1 equals a geometry as a rectangle with width = 10, height = 5 depth= 5.

```
      


#### See also: 

[around](operators-a-to-a#around), [circle](operators-b-to-c#circle), [sphere](operators-s-to-z#sphere), [cone](operators-b-to-c#cone), [line](operators-i-to-m#line), [link](operators-i-to-m#link), [norm](operators-n-to-r#norm), [point](operators-n-to-r#point), [polygon](operators-n-to-r#polygon), [polyline](operators-n-to-r#polyline), [square](operators-s-to-z#square), [cube](operators-b-to-c#cube), [triangle](operators-s-to-z#triangle), 
    	
----

[//]: # (keyword|operator_brewer_colors)
### `brewer_colors`

#### Possible use: 
  *  **`brewer_colors`** (`string`) --->  `list<rgb>`
  * `string` **`brewer_colors`** `int` --->  `list<rgb>`
  *  **`brewer_colors`** (`string` , `int`) --->  `list<rgb>` 

#### Result: 
Build a list of colors of a given type (see website http://colorbrewer2.org/). The list of palettes can be obtained by calling brewer_palettes
Build a list of colors of a given type (see website http://colorbrewer2.org/) with a given number of classes

#### Examples: 
```
 
list<rgb> var0 <- list<rgb> colors <- brewer_colors("OrRd");; // var0 equals a list of 6 blue colors 
list<rgb> var1 <- list<rgb> colors <- brewer_colors("Pastel1", 5);; // var1 equals a list of 5 sequential colors in the palette named 'Pastel1'. The list of palettes can be obtained by calling brewer_palettes

```
      


#### See also: 

[brewer_palettes](operators-b-to-c#brewer_palettes), 
    	
----

[//]: # (keyword|operator_brewer_palettes)
### `brewer_palettes`

#### Possible use: 
  *  **`brewer_palettes`** (`int`) --->  `list<string>`
  * `int` **`brewer_palettes`** `int` --->  `list<string>`
  *  **`brewer_palettes`** (`int` , `int`) --->  `list<string>` 

#### Result: 
returns the list a palette with a given min number of classes)
returns the list a palette with a given min number of classes and max number of classes)

#### Examples: 
```
 
list<string> var0 <- list<string> palettes <- brewer_palettes(3);; // var0 equals a list of palettes that are composed of a min of 3 colors 
list<string> var1 <- list<string> palettes <- brewer_palettes(5,10);; // var1 equals a list of palettes that are composed of a min of 5 colors and a max of 10 colors

```
      


#### See also: 

[brewer_colors](operators-b-to-c#brewer_colors), 
    	
----

[//]: # (keyword|operator_buffer)
### `buffer`
   Same signification as [+](operators-a-to-a#+)
    	
----

[//]: # (keyword|operator_build)
### `build`

#### Possible use: 
  *  **`build`** (`matrix<float>`) --->  `regression`
  * `matrix<float>` **`build`** `string` --->  `regression`
  *  **`build`** (`matrix<float>` , `string`) --->  `regression` 

#### Result: 
returns the regression build from the matrix data (a row = an instance, the last value of each line is the y value) while using the given ordinary least squares method. Usage: build(data)
returns the regression build from the matrix data (a row = an instance, the last value of each line is the y value) while using the given method ("GLS" or "OLS"). Usage: build(data,method)

#### Examples: 
```
matrix([[1,2,3,4],[2,3,4,2]]) build(matrix([[1,2,3,4],[2,3,4,2]]),"GLS") 

```
  
    	
----

[//]: # (keyword|operator_ceil)
### `ceil`

#### Possible use: 
  *  **`ceil`** (`float`) --->  `float` 

#### Result: 
Maps the operand to the smallest following integer, i.e. the smallest integer not less than x.

#### Examples: 
```
 
float var0 <- ceil(3); // var0 equals 3.0 
float var1 <- ceil(3.5); // var1 equals 4.0 
float var2 <- ceil(-4.7); // var2 equals -4.0

```
      


#### See also: 

[floor](operators-d-to-h#floor), [round](operators-n-to-r#round), 
    	
----

[//]: # (keyword|operator_centroid)
### `centroid`

#### Possible use: 
  *  **`centroid`** (`geometry`) --->  `point` 

#### Result: 
Centroid (weighted sum of the centroids of a decomposition of the area into triangles) of the operand-geometry. Can be different to the location of the geometry

#### Examples: 
```
 
point var0 <- centroid(world); // var0 equals the centroid of the square, for example : {50.0,50.0}.

```
      


#### See also: 

[any_location_in](operators-a-to-a#any_location_in), [closest_points_with](operators-b-to-c#closest_points_with), [farthest_point_to](operators-d-to-h#farthest_point_to), [points_at](operators-n-to-r#points_at), 
    	
----

[//]: # (keyword|operator_char)
### `char`

#### Possible use: 
  *  **`char`** (`int`) --->  `string`

#### Special cases:     
  * converts ACSII integer value to character 
  
```
 
string var0 <- char (34); // var0 equals '"'
``` 


    	
----

[//]: # (keyword|operator_chi_square)
### `chi_square`

#### Possible use: 
  * `float` **`chi_square`** `float` --->  `float`
  *  **`chi_square`** (`float` , `float`) --->  `float` 

#### Result: 
Returns the area under the left hand tail (from 0 to x) of the Chi square probability density function with df degrees of freedom.
    	
----

[//]: # (keyword|operator_chi_square_complemented)
### `chi_square_complemented`

#### Possible use: 
  * `float` **`chi_square_complemented`** `float` --->  `float`
  *  **`chi_square_complemented`** (`float` , `float`) --->  `float` 

#### Result: 
Returns the area under the right hand tail (from x to infinity) of the Chi square probability density function with df degrees of freedom.
    	
----

[//]: # (keyword|operator_circle)
### `circle`

#### Possible use: 
  *  **`circle`** (`float`) --->  `geometry`
  * `float` **`circle`** `point` --->  `geometry`
  *  **`circle`** (`float` , `point`) --->  `geometry` 

#### Result: 
A circle geometry which radius is equal to the first operand, and the center has the location equal to the second operand.
A circle geometry which radius is equal to the operand.  

#### Comment: 
the center of the circle is by default the location of the current agent in which has been called this operator.

#### Special cases:     
  * returns a point if the operand is lower or equal to 0.    
  * returns a point if the operand is lower or equal to 0.

#### Examples: 
```
 
geometry var0 <- circle(10,{80,30}); // var0 equals a geometry as a circle of radius 10, the center will be in the location {80,30}. 
geometry var1 <- circle(10); // var1 equals a geometry as a circle of radius 10.

```
      


#### See also: 

[around](operators-a-to-a#around), [cone](operators-b-to-c#cone), [line](operators-i-to-m#line), [link](operators-i-to-m#link), [norm](operators-n-to-r#norm), [point](operators-n-to-r#point), [polygon](operators-n-to-r#polygon), [polyline](operators-n-to-r#polyline), [rectangle](operators-n-to-r#rectangle), [square](operators-s-to-z#square), [triangle](operators-s-to-z#triangle), 
    	
----

[//]: # (keyword|operator_clean)
### `clean`

#### Possible use: 
  *  **`clean`** (`geometry`) --->  `geometry` 

#### Result: 
A geometry corresponding to the cleaning of the operand (geometry, agent, point)  

#### Comment: 
The cleaning corresponds to a buffer with a distance of 0.0

#### Examples: 
```
 
geometry var0 <- clean(self); // var0 equals returns the geometry resulting from the cleaning of the geometry of the agent applying the operator.

```
  
    	
----

[//]: # (keyword|operator_clean_network)
### `clean_network`

#### Possible use: 
  *  **`clean_network`** (`list<geometry>`, `float`, `bool`, `bool`) --->  `list<geometry>` 

#### Result: 
A list of polylines corresponding to the cleaning of the first operand (list of polyline geometry or agents), considering the tolerance distance given by the second operand; the third operator is used to define if the operator should as well split the lines at their intersections(true to split the lines); the last operandis used to specify if the operator should as well keep only the main connected component of the network. Usage: clean_network(lines:list of geometries or agents, tolerance: float, split_lines: bool, keepMainConnectedComponent: bool)  

#### Comment: 
The cleaned set of polylines

#### Examples: 
```
 
list<geometry> var0 <- clean_network(my_road_shapefile.contents, 1.0, true, false); // var0 equals returns the list of polulines resulting from the cleaning of the geometry of the agent applying the operator with a tolerance of 1m, and splitting the lines at their intersections.

```
  
    	
----

[//]: # (keyword|operator_closest_points_with)
### `closest_points_with`

#### Possible use: 
  * `geometry` **`closest_points_with`** `geometry` --->  `list<point>`
  *  **`closest_points_with`** (`geometry` , `geometry`) --->  `list<point>` 

#### Result: 
A list of two closest points between the two geometries.

#### Examples: 
```
 
list<point> var0 <- geom1 closest_points_with(geom2); // var0 equals [pt1, pt2] with pt1 the closest point of geom1 to geom2 and pt1 the closest point of geom2 to geom1

```
      


#### See also: 

[any_location_in](operators-a-to-a#any_location_in), [any_point_in](operators-a-to-a#any_point_in), [farthest_point_to](operators-d-to-h#farthest_point_to), [points_at](operators-n-to-r#points_at), 
    	
----

[//]: # (keyword|operator_closest_to)
### `closest_to`

#### Possible use: 
  * `container<agent>` **`closest_to`** `geometry` --->  `geometry`
  *  **`closest_to`** (`container<agent>` , `geometry`) --->  `geometry`
  *  **`closest_to`** (`container<agent>`, `geometry`, `int`) --->  `list<geometry>` 

#### Result: 
An agent or a geometry among the left-operand list of agents, species or meta-population (addition of species), the closest to the operand (casted as a geometry).
The N agents or geometries among the left-operand list of agents, species or meta-population (addition of species), that are the closest to the operand (casted as a geometry).  

#### Comment: 
the distance is computed in the topology of the calling agent (the agent in which this operator is used), with the distance algorithm specific to the topology.the distance is computed in the topology of the calling agent (the agent in which this operator is used), with the distance algorithm specific to the topology.

#### Examples: 
```
 
geometry var0 <- [ag1, ag2, ag3] closest_to(self); // var0 equals return the closest agent among ag1, ag2 and ag3 to the agent applying the operator.(species1 + species2) closest_to self  
list<geometry> var2 <- [ag1, ag2, ag3] closest_to(self, 2); // var2 equals return the 2 closest agents among ag1, ag2 and ag3 to the agent applying the operator.(species1 + species2) closest_to (self, 5) 

```
      


#### See also: 

[neighbors_at](operators-n-to-r#neighbors_at), [neighbors_of](operators-n-to-r#neighbors_of), [inside](operators-i-to-m#inside), [overlapping](operators-n-to-r#overlapping), [agents_overlapping](operators-a-to-a#agents_overlapping), [agents_inside](operators-a-to-a#agents_inside), [agent_closest_to](operators-a-to-a#agent_closest_to), 
    	
----

[//]: # (keyword|operator_collect)
### `collect`

#### Possible use: 
  * `container` **`collect`** `any expression` --->  `list`
  *  **`collect`** (`container` , `any expression`) --->  `list` 

#### Result: 
returns a new list, in which each element is the evaluation of the right-hand operand.  

#### Comment: 
collect is similar to accumulate except that accumulate always produces flat lists if the right-hand operand returns a list.In addition, collect can be applied to any container.

#### Special cases:     
  * if the left-hand operand is nil, collect throws an error

#### Examples: 
```
 
list var0 <- [1,2,4] collect (each *2); // var0 equals [2,4,8] 
list var1 <- [1,2,4] collect ([2,4]); // var1 equals [[2,4],[2,4],[2,4]] 
list var2 <- [1::2, 3::4, 5::6] collect (each + 2); // var2 equals [4,6,8] 
list var3 <- (list(node) collect (node(each).location.x * 2); // var3 equals the list of nodes with their x multiplied by 2

```
      


#### See also: 

[accumulate](operators-a-to-a#accumulate), 
    	
----

[//]: # (keyword|operator_column_at)
### `column_at`

#### Possible use: 
  * `matrix` **`column_at`** `int` --->  `list`
  *  **`column_at`** (`matrix` , `int`) --->  `list` 

#### Result: 
returns the column at a num_col (right-hand operand)

#### Examples: 
```
 
list var0 <- matrix([["el11","el12","el13"],["el21","el22","el23"],["el31","el32","el33"]]) column_at 2; // var0 equals ["el31","el32","el33"]

```
      


#### See also: 

[row_at](operators-n-to-r#row_at), [rows_list](operators-n-to-r#rows_list), 
    	
----

[//]: # (keyword|operator_columns_list)
### `columns_list`

#### Possible use: 
  *  **`columns_list`** (`matrix`) --->  `list<list>` 

#### Result: 
returns a list of the columns of the matrix, with each column as a list of elements

#### Examples: 
```
 
list<list> var0 <- columns_list(matrix([["el11","el12","el13"],["el21","el22","el23"],["el31","el32","el33"]])); // var0 equals [["el11","el12","el13"],["el21","el22","el23"],["el31","el32","el33"]]

```
      


#### See also: 

[rows_list](operators-n-to-r#rows_list), 
    	
----

[//]: # (keyword|operator_command)
### `command`

#### Possible use: 
  *  **`command`** (`string`) --->  `string`
  * `string` **`command`** `string` --->  `string`
  *  **`command`** (`string` , `string`) --->  `string`
  *  **`command`** (`string`, `string`, `msi.gama.util.GamaMap<java.lang.String,java.lang.String>`) --->  `string` 

#### Result: 
command allows GAMA to issue a system command using the system terminal or shell and to receive a string containing the outcome of the command or script executed. By default, commands are blocking the agent calling them, unless the sequence ' &' is used at the end. In this case, the result of the operator is an empty string
command allows GAMA to issue a system command using the system terminal or shell and to receive a string containing the outcome of the command or script executed. By default, commands are blocking the agent calling them, unless the sequence ' &' is used at the end. In this case, the result of the operator is an empty string. The basic form with only one string in argument uses the directory of the model and does not set any environment variables. Two other forms (with a directory and a map<string, string> of environment variables) are available.
command allows GAMA to issue a system command using the system terminal or shell and to receive a string containing the outcome of the command or script executed. By default, commands are blocking the agent calling them, unless the sequence ' &' is used at the end. In this case, the result of the operator is an empty string. The basic form with only one string in argument uses the directory of the model and does not set any environment variables. Two other forms (with a directory and a map<string, string> of environment variables) are available.
    	
----

[//]: # (keyword|operator_cone)
### `cone`

#### Possible use: 
  *  **`cone`** (`point`) --->  `geometry`
  * `int` **`cone`** `int` --->  `geometry`
  *  **`cone`** (`int` , `int`) --->  `geometry` 

#### Result: 
A cone geometry which min and max angles are given by the operands.
A cone geometry which min and max angles are given by the operands.  

#### Comment: 
the center of the cone is by default the location of the current agent in which has been called this operator.the center of the cone is by default the location of the current agent in which has been called this operator.

#### Special cases:     
  * returns nil if the operand is nil.    
  * returns nil if the operand is nil.

#### Examples: 
```
 
geometry var0 <- cone(0, 45); // var0 equals a geometry as a cone with min angle is 0 and max angle is 45. 
geometry var1 <- cone({0, 45}); // var1 equals a geometry as a cone with min angle is 0 and max angle is 45.

```
      


#### See also: 

[around](operators-a-to-a#around), [circle](operators-b-to-c#circle), [line](operators-i-to-m#line), [link](operators-i-to-m#link), [norm](operators-n-to-r#norm), [point](operators-n-to-r#point), [polygon](operators-n-to-r#polygon), [polyline](operators-n-to-r#polyline), [rectangle](operators-n-to-r#rectangle), [square](operators-s-to-z#square), [triangle](operators-s-to-z#triangle), 
    	
----

[//]: # (keyword|operator_cone3D)
### `cone3D`

#### Possible use: 
  * `float` **`cone3D`** `float` --->  `geometry`
  *  **`cone3D`** (`float` , `float`) --->  `geometry` 

#### Result: 
A cone geometry which base radius size is equal to the first operand, and which the height is equal to the second operand.  

#### Comment: 
the center of the cone is by default the location of the current agent in which has been called this operator.

#### Special cases:     
  * returns a point if the operand is lower or equal to 0.

#### Examples: 
```
 
geometry var0 <- cone3D(10.0,5.0); // var0 equals a geometry as a cone with a base circle of radius 10 and a height of 5.

```
      


#### See also: 

[around](operators-a-to-a#around), [cone](operators-b-to-c#cone), [line](operators-i-to-m#line), [link](operators-i-to-m#link), [norm](operators-n-to-r#norm), [point](operators-n-to-r#point), [polygon](operators-n-to-r#polygon), [polyline](operators-n-to-r#polyline), [rectangle](operators-n-to-r#rectangle), [square](operators-s-to-z#square), [triangle](operators-s-to-z#triangle), 
    	
----

[//]: # (keyword|operator_connected_components_of)
### `connected_components_of`

#### Possible use: 
  *  **`connected_components_of`** (`graph`) --->  `list<list>`
  * `graph` **`connected_components_of`** `bool` --->  `list<list>`
  *  **`connected_components_of`** (`graph` , `bool`) --->  `list<list>` 

#### Result: 
returns the connected components of a graph, i.e. the list of all vertices that are in the maximally connected component together with the specified vertex. 
returns the connected components of a graph, i.e. the list of all edges (if the boolean is true) or vertices (if the boolean is false) that are in the connected components.

#### Examples: 
```
graph my_graph <- graph([]);  
list<list> var1 <- connected_components_of (my_graph); // var1 equals the list of all the components as listgraph my_graph2 <- graph([]);  
list<list> var3 <- connected_components_of (my_graph2, true); // var3 equals the list of all the components as list

```
      


#### See also: 

[alpha_index](operators-a-to-a#alpha_index), [connectivity_index](operators-b-to-c#connectivity_index), [nb_cycles](operators-n-to-r#nb_cycles), 
    	
----

[//]: # (keyword|operator_connectivity_index)
### `connectivity_index`

#### Possible use: 
  *  **`connectivity_index`** (`graph`) --->  `float` 

#### Result: 
returns a simple connectivity index. This number is estimated through the number of nodes (v) and of sub-graphs (p) : IC = (v - p) /(v - 1).

#### Examples: 
```
graph graphEpidemio <- graph([]);  
float var1 <- connectivity_index(graphEpidemio); // var1 equals the connectivity index of the graph

```
      


#### See also: 

[alpha_index](operators-a-to-a#alpha_index), [beta_index](operators-b-to-c#beta_index), [gamma_index](operators-d-to-h#gamma_index), [nb_cycles](operators-n-to-r#nb_cycles), 
    	
----

[//]: # (keyword|operator_container)
### `container`

#### Possible use: 
  *  **`container`** (`any`) --->  `container` 

#### Result: 
Casts the operand into the type container
    	
----

[//]: # (keyword|operator_contains)
### `contains`

#### Possible use: 
  * `container<KeyType,ValueType>` **`contains`** `unknown` --->  `bool`
  *  **`contains`** (`container<KeyType,ValueType>` , `unknown`) --->  `bool`
  * `string` **`contains`** `string` --->  `bool`
  *  **`contains`** (`string` , `string`) --->  `bool` 

#### Result: 
true, if the container contains the right operand, false otherwise  

#### Comment: 
the contains operator behavior depends on the nature of the operand

#### Special cases:     
  * if it is a map, contains returns true if the operand is a key of the map    
  * if it is a file, contains returns true it the operand is contained in the file content    
  * if it is a population, contains returns true if the operand is an agent of the population, false otherwise    
  * if it is a graph, contains returns true if the operand is a node or an edge of the graph, false otherwise    
  * if both operands are strings, returns true if the right-hand operand contains the right-hand pattern;    
  * if it is a list or a matrix, contains returns true if the list or matrix contains the right operand 
  
```
 
bool var0 <- [1, 2, 3] contains 2; // var0 equals true 
bool var1 <- [{1,2}, {3,4}, {5,6}] contains {3,4}; // var1 equals true
``` 



#### Examples: 
```
 
bool var2 <- 'abcded' contains 'bc'; // var2 equals true

```
      


#### See also: 

[contains_all](operators-b-to-c#contains_all), [contains_any](operators-b-to-c#contains_any), 
    	
----

[//]: # (keyword|operator_contains_all)
### `contains_all`

#### Possible use: 
  * `string` **`contains_all`** `list` --->  `bool`
  *  **`contains_all`** (`string` , `list`) --->  `bool`
  * `container` **`contains_all`** `container` --->  `bool`
  *  **`contains_all`** (`container` , `container`) --->  `bool` 

#### Result: 
true if the left operand contains all the elements of the right operand, false otherwise  

#### Comment: 
the definition of contains depends on the container

#### Special cases:     
  * if the right operand is nil or empty, contains_all returns true    
  * if the left-operand is a string, test whether the string contains all the element of the list; 
  
```
 
bool var0 <- "abcabcabc" contains_all ["ca","xy"]; // var0 equals false
``` 



#### Examples: 
```
 
bool var1 <- [1,2,3,4,5,6] contains_all [2,4]; // var1 equals true  
bool var2 <- [1,2,3,4,5,6] contains_all [2,8]; // var2 equals false 
bool var3 <- [1::2, 3::4, 5::6] contains_all [1,3]; // var3 equals false  
bool var4 <- [1::2, 3::4, 5::6] contains_all [2,4]; // var4 equals true

```
      


#### See also: 

[contains](operators-b-to-c#contains), [contains_any](operators-b-to-c#contains_any), 
    	
----

[//]: # (keyword|operator_contains_any)
### `contains_any`

#### Possible use: 
  * `string` **`contains_any`** `list` --->  `bool`
  *  **`contains_any`** (`string` , `list`) --->  `bool`
  * `container` **`contains_any`** `container` --->  `bool`
  *  **`contains_any`** (`container` , `container`) --->  `bool` 

#### Result: 
true if the left operand contains one of the elements of the right operand, false otherwise  

#### Comment: 
the definition of contains depends on the container

#### Special cases:     
  * if the right operand is nil or empty, contains_any returns false

#### Examples: 
```
 
bool var0 <- "abcabcabc" contains_any ["ca","xy"]; // var0 equals true 
bool var1 <- [1,2,3,4,5,6] contains_any [2,4]; // var1 equals true  
bool var2 <- [1,2,3,4,5,6] contains_any [2,8]; // var2 equals true 
bool var3 <- [1::2, 3::4, 5::6] contains_any [1,3]; // var3 equals false 
bool var4 <- [1::2, 3::4, 5::6] contains_any [2,4]; // var4 equals true

```
      


#### See also: 

[contains](operators-b-to-c#contains), [contains_all](operators-b-to-c#contains_all), 
    	
----

[//]: # (keyword|operator_contains_edge)
### `contains_edge`

#### Possible use: 
  * `graph` **`contains_edge`** `unknown` --->  `bool`
  *  **`contains_edge`** (`graph` , `unknown`) --->  `bool`
  * `graph` **`contains_edge`** `pair` --->  `bool`
  *  **`contains_edge`** (`graph` , `pair`) --->  `bool` 

#### Result: 
returns true if the graph(left-hand operand) contains the given edge (righ-hand operand), false otherwise

#### Special cases:     
  * if the left-hand operand is nil, returns false    
  * if the right-hand operand is a pair, returns true if it exists an edge between the two elements of the pair in the graph 
  
```
 
bool var2 <- graphEpidemio contains_edge (node(0)::node(3)); // var2 equals true
``` 



#### Examples: 
```
graph graphFromMap <-  as_edge_graph([{1,5}::{12,45},{12,45}::{34,56}]);  
bool var1 <- graphFromMap contains_edge link({1,5},{12,45}); // var1 equals true

```
      


#### See also: 

[contains_vertex](operators-b-to-c#contains_vertex), 
    	
----

[//]: # (keyword|operator_contains_vertex)
### `contains_vertex`

#### Possible use: 
  * `graph` **`contains_vertex`** `unknown` --->  `bool`
  *  **`contains_vertex`** (`graph` , `unknown`) --->  `bool` 

#### Result: 
returns true if the graph(left-hand operand) contains the given vertex (righ-hand operand), false otherwise

#### Special cases:     
  * if the left-hand operand is nil, returns false

#### Examples: 
```
graph graphFromMap<-  as_edge_graph([{1,5}::{12,45},{12,45}::{34,56}]);  
bool var1 <- graphFromMap contains_vertex {1,5}; // var1 equals true

```
      


#### See also: 

[contains_edge](operators-b-to-c#contains_edge), 
    	
----

[//]: # (keyword|operator_conversation)
### `conversation`

#### Possible use: 
  *  **`conversation`** (`unknown`) --->  `conversation`
    	
----

[//]: # (keyword|operator_convex_hull)
### `convex_hull`

#### Possible use: 
  *  **`convex_hull`** (`geometry`) --->  `geometry` 

#### Result: 
A geometry corresponding to the convex hull of the operand.

#### Examples: 
```
 
geometry var0 <- convex_hull(self); // var0 equals the convex hull of the geometry of the agent applying the operator

```
  
    	
----

[//]: # (keyword|operator_copy)
### `copy`

#### Possible use: 
  *  **`copy`** (`unknown`) --->  `unknown` 

#### Result: 
returns a copy of the operand.
    	
----

[//]: # (keyword|operator_copy_between)
### `copy_between`

#### Possible use: 
  *  **`copy_between`** (`string`, `int`, `int`) --->  `string`
  *  **`copy_between`** (`list`, `int`, `int`) --->  `list` 

#### Result: 
Returns a copy of the first operand between the indexes determined by the second (inclusive) and third operands (exclusive)

#### Special cases:     
  * If the first operand is empty, returns an empty object of the same type    
  * If the second operand is greater than or equal to the third operand, return an empty object of the same type    
  * If the first operand is nil, raises an error

#### Examples: 
```
 
string var0 <- copy_between("abcabcabc", 2,6); // var0 equals "cabc" 
list var1 <-  copy_between ([4, 1, 6, 9 ,7], 1, 3); // var1 equals [1, 6]

```
  
    	
----

[//]: # (keyword|operator_corR)
### `corR`

#### Possible use: 
  * `container` **`corR`** `container` --->  `unknown`
  *  **`corR`** (`container` , `container`) --->  `unknown` 

#### Result: 
returns the Pearson correlation coefficient of two given vectors (right-hand operands) in given variable  (left-hand operand).

#### Special cases:     
  * if the lengths of two vectors in the right-hand aren't equal, returns 0

#### Examples: 
```
list X <- [1, 2, 3]; list Y <- [1, 2, 4];  
unknown var2 <- corR(X, Y); // var2 equals 0.981980506061966

```
  
    	
----

[//]: # (keyword|operator_correlation)
### `correlation`

#### Possible use: 
  * `container` **`correlation`** `container` --->  `float`
  *  **`correlation`** (`container` , `container`) --->  `float` 

#### Result: 
Returns the correlation of two data sequences
    	
----

[//]: # (keyword|operator_cos)
### `cos`

#### Possible use: 
  *  **`cos`** (`int`) --->  `float`
  *  **`cos`** (`float`) --->  `float` 

#### Result: 
Returns the value (in [-1,1]) of the cosinus of the operand (in decimal degrees).  The argument is casted to an int before being evaluated.

#### Special cases:     
  * Operand values out of the range [0-359] are normalized.

#### Examples: 
```
 
float var0 <- cos (0); // var0 equals 1.0 
float var1 <- cos(360); // var1 equals 1.0 
float var2 <- cos(-720); // var2 equals 1.0

```
      


#### See also: 

[sin](operators-s-to-z#sin), [tan](operators-s-to-z#tan), 
    	
----

[//]: # (keyword|operator_cos_rad)
### `cos_rad`

#### Possible use: 
  *  **`cos_rad`** (`float`) --->  `float` 

#### Result: 
Returns the value (in [-1,1]) of the cosinus of the operand (in radians).

#### Special cases:     
  * Operand values out of the range [0-359] are normalized.    


#### See also: 

[sin](operators-s-to-z#sin), [tan](operators-s-to-z#tan), 
    	
----

[//]: # (keyword|operator_count)
### `count`

#### Possible use: 
  * `container` **`count`** `any expression` --->  `int`
  *  **`count`** (`container` , `any expression`) --->  `int` 

#### Result: 
returns an int, equal to the number of elements of the left-hand operand that make the right-hand operand evaluate to true.  

#### Comment: 
in the right-hand operand, the keyword each can be used to represent, in turn, each of the elements.

#### Special cases:     
  * if the left-hand operand is nil, count throws an error

#### Examples: 
```
 
int var0 <- [1,2,3,4,5,6,7,8] count (each > 3); // var0 equals 5// Number of nodes of graph g2 without any out edge graph g2 <- graph([]);  
int var3 <- g2 count (length(g2 out_edges_of each) = 0  ) ; // var3 equals the total number of out edges// Number of agents node with x > 32 int n <- (list(node) count (round(node(each).location.x) > 32);  
int var6 <- [1::2, 3::4, 5::6] count (each > 4); // var6 equals 1

```
      


#### See also: 

[group_by](operators-d-to-h#group_by), 
    	
----

[//]: # (keyword|operator_covariance)
### `covariance`

#### Possible use: 
  * `container` **`covariance`** `container` --->  `float`
  *  **`covariance`** (`container` , `container`) --->  `float` 

#### Result: 
Returns the covariance of two data sequences
    	
----

[//]: # (keyword|operator_covers)
### `covers`

#### Possible use: 
  * `geometry` **`covers`** `geometry` --->  `bool`
  *  **`covers`** (`geometry` , `geometry`) --->  `bool` 

#### Result: 
A boolean, equal to true if the left-geometry (or agent/point) covers the right-geometry (or agent/point).

#### Special cases:     
  * if one of the operand is null, returns false.

#### Examples: 
```
 
bool var0 <- square(5) covers square(2); // var0 equals true

```
      


#### See also: 

[disjoint_from](operators-d-to-h#disjoint_from), [crosses](operators-b-to-c#crosses), [overlaps](operators-n-to-r#overlaps), [partially_overlaps](operators-n-to-r#partially_overlaps), [touches](operators-s-to-z#touches), 
    	
----

[//]: # (keyword|operator_create_map)
### `create_map`

#### Possible use: 
  * `list` **`create_map`** `list` --->  `map`
  *  **`create_map`** (`list` , `list`) --->  `map` 

#### Result: 
returns a new map using the left operand as keys for the right operand

#### Special cases:     
  * if the left operand contains duplicates, create_map throws an error.    
  * if both operands have different lengths, choose the minimum length between the two operandsfor the size of the map

#### Examples: 
```
 
map<int,string> var0 <- create_map([0,1,2],['a','b','c']); // var0 equals [0::'a',1::'b',2::'c'] 
map<int,float> var1 <- create_map([0,1],[0.1,0.2,0.3]); // var1 equals [0::0.1,1::0.2] 
map<string,float> var2 <- create_map(['a','b','c','d'],[1.0,2.0,3.0]); // var2 equals ['a'::1.0,'b'::2.0,'c'::3.0]

```
  
    	
----

[//]: # (keyword|operator_cross)
### `cross`

#### Possible use: 
  *  **`cross`** (`float`) --->  `geometry`
  * `float` **`cross`** `float` --->  `geometry`
  *  **`cross`** (`float` , `float`) --->  `geometry` 

#### Result: 
A cross, which radius is equal to the first operand
A cross, which radius is equal to the first operand and the width of the lines for the second

#### Examples: 
```
 
geometry var0 <- cross(10); // var0 equals a geometry as a cross of radius 10 
geometry var1 <- cross(10,2); // var1 equals a geometry as a cross of radius 10, and with a width of 2 for the lines 

```
      


#### See also: 

[around](operators-a-to-a#around), [cone](operators-b-to-c#cone), [line](operators-i-to-m#line), [link](operators-i-to-m#link), [norm](operators-n-to-r#norm), [point](operators-n-to-r#point), [polygon](operators-n-to-r#polygon), [polyline](operators-n-to-r#polyline), [super_ellipse](operators-s-to-z#super_ellipse), [rectangle](operators-n-to-r#rectangle), [square](operators-s-to-z#square), [circle](operators-b-to-c#circle), [ellipse](operators-d-to-h#ellipse), [triangle](operators-s-to-z#triangle), 
    	
----

[//]: # (keyword|operator_crosses)
### `crosses`

#### Possible use: 
  * `geometry` **`crosses`** `geometry` --->  `bool`
  *  **`crosses`** (`geometry` , `geometry`) --->  `bool` 

#### Result: 
A boolean, equal to true if the left-geometry (or agent/point) crosses the right-geometry (or agent/point).

#### Special cases:     
  * if one of the operand is null, returns false.    
  * if one operand is a point, returns false.

#### Examples: 
```
 
bool var0 <- polyline([{10,10},{20,20}]) crosses polyline([{10,20},{20,10}]); // var0 equals true 
bool var1 <- polyline([{10,10},{20,20}]) crosses {15,15}; // var1 equals true 
bool var2 <- polyline([{0,0},{25,25}]) crosses polygon([{10,10},{10,20},{20,20},{20,10}]); // var2 equals true

```
      


#### See also: 

[disjoint_from](operators-d-to-h#disjoint_from), [intersects](operators-i-to-m#intersects), [overlaps](operators-n-to-r#overlaps), [partially_overlaps](operators-n-to-r#partially_overlaps), [touches](operators-s-to-z#touches), 
    	
----

[//]: # (keyword|operator_crs)
### `crs`

#### Possible use: 
  *  **`crs`** (`file`) --->  `string` 

#### Result: 
the Coordinate Reference System (CRS) of the GIS file

#### Examples: 
```
 
string var0 <- crs(my_shapefile); // var0 equals the crs of the shapefile

```
  
    	
----

[//]: # (keyword|operator_CRS_transform)
### `CRS_transform`

#### Possible use: 
  *  **`CRS_transform`** (`geometry`) --->  `geometry`
  * `geometry` **`CRS_transform`** `string` --->  `geometry`
  *  **`CRS_transform`** (`geometry` , `string`) --->  `geometry`

#### Special cases:     
  * returns the geometry corresponding to the transformation of the given geometry by the left operand CRS (Coordinate Reference System) 
  
```
 
geometry var0 <- shape CRS_transform("EPSG:4326"); // var0 equals a geometry corresponding to the agent geometry transformed into the EPSG:4326 CRS
``` 

    
  * returns the geometry corresponding to the transformation of the given geometry by the current CRS (Coordinate Reference System), the one corresponding to the world's agent one 
  
```
 
geometry var1 <- CRS_transform(shape); // var1 equals a geometry corresponding to the agent geometry transformed into the current CRS
``` 


    	
----

[//]: # (keyword|operator_csv_file)
### `csv_file`

#### Possible use: 
  *  **`csv_file`** (`string`) --->  `file` 

#### Result: 
Constructs a file of type csv. Allowed extensions are limited to csv, tsv
    	
----

[//]: # (keyword|operator_cube)
### `cube`

#### Possible use: 
  *  **`cube`** (`float`) --->  `geometry` 

#### Result: 
A cube geometry which side size is equal to the operand.  

#### Comment: 
the center of the cube is by default the location of the current agent in which has been called this operator.

#### Special cases:     
  * returns nil if the operand is nil.

#### Examples: 
```
 
geometry var0 <- cube(10); // var0 equals a geometry as a square of side size 10.

```
      


#### See also: 

[around](operators-a-to-a#around), [circle](operators-b-to-c#circle), [cone](operators-b-to-c#cone), [line](operators-i-to-m#line), [link](operators-i-to-m#link), [norm](operators-n-to-r#norm), [point](operators-n-to-r#point), [polygon](operators-n-to-r#polygon), [polyline](operators-n-to-r#polyline), [rectangle](operators-n-to-r#rectangle), [triangle](operators-s-to-z#triangle), 
    	
----

[//]: # (keyword|operator_curve)
### `curve`

#### Possible use: 
  *  **`curve`** (`point`, `point`, `point`) --->  `geometry`
  *  **`curve`** (`point`, `point`, `float`) --->  `geometry`
  *  **`curve`** (`point`, `point`, `point`, `int`) --->  `geometry`
  *  **`curve`** (`point`, `point`, `float`, `float`) --->  `geometry`
  *  **`curve`** (`point`, `point`, `float`, `bool`) --->  `geometry`
  *  **`curve`** (`point`, `point`, `point`, `point`) --->  `geometry`
  *  **`curve`** (`point`, `point`, `float`, `bool`, `int`) --->  `geometry`
  *  **`curve`** (`point`, `point`, `point`, `point`, `int`) --->  `geometry`
  *  **`curve`** (`point`, `point`, `float`, `int`, `float`) --->  `geometry`
  *  **`curve`** (`point`, `point`, `float`, `int`, `float`, `float`) --->  `geometry`
  *  **`curve`** (`point`, `point`, `float`, `bool`, `int`, `float`) --->  `geometry` 

#### Result: 
A cubic Bezier curve geometry built from the two given points with the given coefficient for the radius and composed of the given number of points, considering the given inflection point (between 0.0 and 1.0 - default 0.5), and the given rotation angle (90 = along the z axis).
A quadratic Bezier curve geometry built from the three given points composed of a given numnber of points.
A cubic Bezier curve geometry built from the two given points with the given coefficient for the radius considering the given rotation angle (90 = along the z axis).
A cubic Bezier curve geometry built from the two given points with the given coefficient for the radius and composed of the given number of points - the boolean is used to specified if it is the right side.
A quadratic Bezier curve geometry built from the three given points composed of 10 points.
A cubic Bezier curve geometry built from the four given points composed of a given number of points.
A cubic Bezier curve geometry built from the two given points with the given coefficient for the radius and composed of the given number of points, considering the given rotation angle (90 = along the z axis).
A cubic Bezier curve geometry built from the two given points with the given coefficient for the radius and composed of 10 points - the last boolean is used to specified if it is the right side.
A cubic Bezier curve geometry built from the two given points with the given coefficient for the radius and composed of the given number of points - the boolean is used to specified if it is the right side and the last value to indicate where is the inflection point (between 0.0 and 1.0 - default 0.5).
A cubic Bezier curve geometry built from the two given points with the given coefficient for the radius and composed of 10 points.
A cubic Bezier curve geometry built from the four given points composed of 10 points.

#### Special cases:     
  * if the operand is nil, returns nil    
  * if the operand is nil, returns nil    
  * if the last operand (number of points) is inferior to 2, returns nil    
  * if the operand is nil, returns nil    
  * if the operand is nil, returns nil    
  * if the operand is nil, returns nil    
  * if the operand is nil, returns nil    
  * if the last operand (number of points) is inferior to 2, returns nil    
  * if the operand is nil, returns nil    
  * if the operand is nil, returns nil    
  * if the operand is nil, returns nil    
  * if the operand is nil, returns nil    
  * if the operand is nil, returns nil

#### Examples: 
```
 
geometry var0 <- curve({0,0},{10,10}, 0.5, 100, 0.8, 90); // var0 equals a cubic Bezier curve geometry composed of 100 points from p0 to p1 at the right side. 
geometry var1 <- curve({0,0}, {0,10}, {10,10}, 20); // var1 equals a quadratic Bezier curve geometry composed of 20 points from p0 to p2. 
geometry var2 <- curve({0,0},{10,10}, 0.5, 90); // var2 equals a cubic Bezier curve geometry composed of 100 points from p0 to p1 at the right side. 
geometry var3 <- curve({0,0},{10,10}, 0.5, false, 100); // var3 equals a cubic Bezier curve geometry composed of 100 points from p0 to p1 at the right side. 
geometry var4 <- curve({0,0}, {0,10}, {10,10}); // var4 equals a quadratic Bezier curve geometry composed of 10 points from p0 to p2. 
geometry var5 <- curve({0,0}, {0,10}, {10,10}); // var5 equals a cubic Bezier curve geometry composed of 10 points from p0 to p3. 
geometry var6 <- curve({0,0},{10,10}, 0.5, 100, 90); // var6 equals a cubic Bezier curve geometry composed of 100 points from p0 to p1 at the right side. 
geometry var7 <- curve({0,0},{10,10}, 0.5, false); // var7 equals a cubic Bezier curve geometry composed of 10 points from p0 to p1 at the left side. 
geometry var8 <- curve({0,0},{10,10}, 0.5, false, 100, 0.8); // var8 equals a cubic Bezier curve geometry composed of 100 points from p0 to p1 at the right side. 
geometry var9 <- curve({0,0},{10,10}, 0.5); // var9 equals a cubic Bezier curve geometry composed of 10 points from p0 to p1. 
geometry var10 <- curve({0,0}, {0,10}, {10,10}); // var10 equals a cubic Bezier curve geometry composed of 10 points from p0 to p3.

```
      


#### See also: 

[around](operators-a-to-a#around), [circle](operators-b-to-c#circle), [cone](operators-b-to-c#cone), [link](operators-i-to-m#link), [norm](operators-n-to-r#norm), [point](operators-n-to-r#point), [polygone](operators-s-to-z#polygone), [rectangle](operators-n-to-r#rectangle), [square](operators-s-to-z#square), [triangle](operators-s-to-z#triangle), [line](operators-i-to-m#line), 
    	
----

[//]: # (keyword|operator_cylinder)
### `cylinder`

#### Possible use: 
  * `float` **`cylinder`** `float` --->  `geometry`
  *  **`cylinder`** (`float` , `float`) --->  `geometry` 

#### Result: 
A cylinder geometry which radius is equal to the operand.  

#### Comment: 
the center of the cylinder is by default the location of the current agent in which has been called this operator.

#### Special cases:     
  * returns a point if the operand is lower or equal to 0.

#### Examples: 
```
 
geometry var0 <- cylinder(10,10); // var0 equals a geometry as a circle of radius 10.

```
      


#### See also: 

[around](operators-a-to-a#around), [cone](operators-b-to-c#cone), [line](operators-i-to-m#line), [link](operators-i-to-m#link), [norm](operators-n-to-r#norm), [point](operators-n-to-r#point), [polygon](operators-n-to-r#polygon), [polyline](operators-n-to-r#polyline), [rectangle](operators-n-to-r#rectangle), [square](operators-s-to-z#square), [triangle](operators-s-to-z#triangle), 