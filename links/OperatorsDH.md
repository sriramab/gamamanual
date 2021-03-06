# Operators (D to H)
 	

----

[//]: # (keyword|operator_date)
### `date`

#### Possible use: 
  * `string` **`date`** `string` --->  `date`
  *  **`date`** (`string` , `string`) --->  `date`
  *  **`date`** (`string`, `string`, `string`) --->  `date` 

#### Result: 
converts a string to a date following a custom pattern and a specific locale (e.g. 'fr', 'en'...). The pattern can use "%Y %M %N %D %E %h %m %s %z" for parsing years, months, name of month, days, name of days, hours, minutes, seconds and the time-zone. A null or empty pattern will parse the date using one of the ISO date & time formats (similar to date('...') in that case). The pattern can also follow the pattern definition found here, which gives much more control over what will be parsed: https://docs.oracle.com/javase/8/docs/api/java/time/format/DateTimeFormatter.html#patterns. Different patterns are available by default as constant: #iso_local, #iso_simple, #iso_offset, #iso_zoned and #custom, which can be changed in the preferences 
converts a string to a date following a custom pattern. The pattern can use "%Y %M %N %D %E %h %m %s %z" for outputting years, months, name of month, days, name of days, hours, minutes, seconds and the time-zone. A null or empty pattern will parse the date using one of the ISO date & time formats (similar to date('...') in that case). The pattern can also follow the pattern definition found here, which gives much more control over what will be parsed: https://docs.oracle.com/javase/8/docs/api/java/time/format/DateTimeFormatter.html#patterns. Different patterns are available by default as constant: #iso_local, #iso_simple, #iso_offset, #iso_zoned and #custom, which can be changed in the preferences

#### Examples: 
```
date d <- date("1999-january-30", 'yyyy-MMMM-dd', 'en'); date den <- date("1999-12-30", 'yyyy-MM-dd'); 

```
  
    	
----

[//]: # (keyword|operator_dbscan)
### `dbscan`

#### Possible use: 
  *  **`dbscan`** (`list`, `float`, `int`) --->  `list<list>` 

#### Result: 
returns the list of clusters (list of instance indices) computed with the dbscan (density-based spatial clustering of applications with noise) algorithm from the first operand data according to the maximum radius of the neighborhood to be considered (eps) and the minimum number of points needed for a cluster (minPts). Usage: dbscan(data,eps,minPoints)

#### Special cases:     
  * if the lengths of two vectors in the right-hand aren't equal, returns 0

#### Examples: 
```
 
list<list> var0 <- dbscan ([[2,4,5], [3,8,2], [1,1,3], [4,3,4]],10,2); // var0 equals []

```
  
    	
----

[//]: # (keyword|operator_dead)
### `dead`

#### Possible use: 
  *  **`dead`** (`agent`) --->  `bool` 

#### Result: 
true if the agent is dead (or null), false otherwise.

#### Examples: 
```
 
bool var0 <- dead(agent_A); // var0 equals true or false

```
  
    	
----

[//]: # (keyword|operator_degree_of)
### `degree_of`

#### Possible use: 
  * `graph` **`degree_of`** `unknown` --->  `int`
  *  **`degree_of`** (`graph` , `unknown`) --->  `int` 

#### Result: 
returns the degree (in+out) of a vertex (right-hand operand) in the graph given as left-hand operand.

#### Examples: 
```
 
int var1 <- graphFromMap degree_of (node(3)); // var1 equals 3

```
      


#### See also: 

[in_degree_of](operators-i-to-m#in_degree_of), [out_degree_of](operators-n-to-r#out_degree_of), 
    	
----

[//]: # (keyword|operator_dem)
### `dem`

#### Possible use: 
  *  **`dem`** (`file`) --->  `geometry`
  * `file` **`dem`** `file` --->  `geometry`
  *  **`dem`** (`file` , `file`) --->  `geometry`
  * `file` **`dem`** `float` --->  `geometry`
  *  **`dem`** (`file` , `float`) --->  `geometry`
  *  **`dem`** (`file`, `file`, `float`) --->  `geometry` 

#### Result: 
A polygon that is equivalent to the surface of the texture

#### Examples: 
```
 
geometry var0 <- dem(dem); // var0 equals returns a geometry as a rectangle of width and height equal to the texture. 
geometry var1 <- dem(dem,texture); // var1 equals a geometry as a rectangle of weight and height equal to the texture. 
geometry var2 <- dem(dem,z_factor); // var2 equals a geometry as a rectangle of weight and height equal to the texture. 
geometry var3 <- dem(dem,texture,z_factor); // var3 equals a geometry as a rectangle of width and height equal to the texture.

```
  
    	
----

[//]: # (keyword|operator_det)
### `det`
   Same signification as [determinant](operators-d-to-h#determinant)
    	
----

[//]: # (keyword|operator_determinant)
### `determinant`

#### Possible use: 
  *  **`determinant`** (`matrix`) --->  `float` 

#### Result: 
The determinant of the given matrix

#### Examples: 
```
 
float var0 <- determinant(matrix([[1,2],[3,4]])); // var0 equals -2

```
  
    	
----

[//]: # (keyword|operator_diff)
### `diff`

#### Possible use: 
  * `float` **`diff`** `float` --->  `float`
  *  **`diff`** (`float` , `float`) --->  `float` 

#### Result: 
A placeholder function for expressing equations
    	
----

[//]: # (keyword|operator_diff2)
### `diff2`

#### Possible use: 
  * `float` **`diff2`** `float` --->  `float`
  *  **`diff2`** (`float` , `float`) --->  `float` 

#### Result: 
A placeholder function for expressing equations
    	
----

[//]: # (keyword|operator_directed)
### `directed`

#### Possible use: 
  *  **`directed`** (`graph`) --->  `graph` 

#### Result: 
the operand graph becomes a directed graph.  

#### Comment: 
the operator alters the operand graph, it does not create a new one.    


#### See also: 

[undirected](operators-s-to-z#undirected), 
    	
----

[//]: # (keyword|operator_direction_between)
### `direction_between`

#### Possible use: 
  * `topology` **`direction_between`** `container<geometry>` --->  `float`
  *  **`direction_between`** (`topology` , `container<geometry>`) --->  `float` 

#### Result: 
A direction (in degree) between a list of two geometries (geometries, agents, points) considering a topology.

#### Examples: 
```
 
float var0 <- my_topology direction_between [ag1, ag2]; // var0 equals the direction between ag1 and ag2 considering the topology my_topology

```
      


#### See also: 

[towards](operators-s-to-z#towards), [direction_to](operators-d-to-h#direction_to), [distance_to](operators-d-to-h#distance_to), [distance_between](operators-d-to-h#distance_between), [path_between](operators-n-to-r#path_between), [path_to](operators-n-to-r#path_to), 
    	
----

[//]: # (keyword|operator_direction_to)
### `direction_to`
   Same signification as [towards](operators-s-to-z#towards)
    	
----

[//]: # (keyword|operator_disjoint_from)
### `disjoint_from`

#### Possible use: 
  * `geometry` **`disjoint_from`** `geometry` --->  `bool`
  *  **`disjoint_from`** (`geometry` , `geometry`) --->  `bool` 

#### Result: 
A boolean, equal to true if the left-geometry (or agent/point) is disjoints from the right-geometry (or agent/point).

#### Special cases:     
  * if one of the operand is null, returns true.    
  * if one operand is a point, returns false if the point is included in the geometry.

#### Examples: 
```
 
bool var0 <- polyline([{10,10},{20,20}]) disjoint_from polyline([{15,15},{25,25}]); // var0 equals false 
bool var1 <- polygon([{10,10},{10,20},{20,20},{20,10}]) disjoint_from polygon([{15,15},{15,25},{25,25},{25,15}]); // var1 equals false 
bool var2 <- polygon([{10,10},{10,20},{20,20},{20,10}]) disjoint_from {15,15}; // var2 equals false 
bool var3 <- polygon([{10,10},{10,20},{20,20},{20,10}]) disjoint_from {25,25}; // var3 equals true 
bool var4 <- polygon([{10,10},{10,20},{20,20},{20,10}]) disjoint_from polygon([{35,35},{35,45},{45,45},{45,35}]); // var4 equals true

```
      


#### See also: 

[intersects](operators-i-to-m#intersects), [crosses](operators-b-to-c#crosses), [overlaps](operators-n-to-r#overlaps), [partially_overlaps](operators-n-to-r#partially_overlaps), [touches](operators-s-to-z#touches), 
    	
----

[//]: # (keyword|operator_distance_between)
### `distance_between`

#### Possible use: 
  * `topology` **`distance_between`** `container<geometry>` --->  `float`
  *  **`distance_between`** (`topology` , `container<geometry>`) --->  `float` 

#### Result: 
A distance between a list of geometries (geometries, agents, points) considering a topology.

#### Examples: 
```
 
float var0 <- my_topology distance_between [ag1, ag2, ag3]; // var0 equals the distance between ag1, ag2 and ag3 considering the topology my_topology

```
      


#### See also: 

[towards](operators-s-to-z#towards), [direction_to](operators-d-to-h#direction_to), [distance_to](operators-d-to-h#distance_to), [direction_between](operators-d-to-h#direction_between), [path_between](operators-n-to-r#path_between), [path_to](operators-n-to-r#path_to), 
    	
----

[//]: # (keyword|operator_distance_to)
### `distance_to`

#### Possible use: 
  * `point` **`distance_to`** `point` --->  `float`
  *  **`distance_to`** (`point` , `point`) --->  `float`
  * `geometry` **`distance_to`** `geometry` --->  `float`
  *  **`distance_to`** (`geometry` , `geometry`) --->  `float` 

#### Result: 
A distance between two geometries (geometries, agents or points) considering the topology of the agent applying the operator.

#### Examples: 
```
 
float var0 <- ag1 distance_to ag2; // var0 equals the distance between ag1 and ag2 considering the topology of the agent applying the operator

```
      


#### See also: 

[towards](operators-s-to-z#towards), [direction_to](operators-d-to-h#direction_to), [distance_between](operators-d-to-h#distance_between), [direction_between](operators-d-to-h#direction_between), [path_between](operators-n-to-r#path_between), [path_to](operators-n-to-r#path_to), 
    	
----

[//]: # (keyword|operator_distinct)
### `distinct`

#### Possible use: 
  *  **`distinct`** (`container`) --->  `list` 

#### Result: 
produces a set from the elements of the operand (i.e. a list without duplicated elements)

#### Special cases:     
  * if the operand is nil, remove_duplicates returns nil    
  * if the operand is a graph, remove_duplicates returns the set of nodes    
  * if the operand is a matrix, remove_duplicates returns a matrix without duplicated row    
  * if the operand is a map, remove_duplicates returns the set of values without duplicate 
  
```
 
list var1 <- remove_duplicates([1::3,2::4,3::3,5::7]); // var1 equals [3,4,7]
``` 



#### Examples: 
```
 
list var0 <- remove_duplicates([3,2,5,1,2,3,5,5,5]); // var0 equals [3,2,5,1]

```
  
    	
----

[//]: # (keyword|operator_distribution_of)
### `distribution_of`

#### Possible use: 
  *  **`distribution_of`** (`container`) --->  `map`
  * `container` **`distribution_of`** `int` --->  `map`
  *  **`distribution_of`** (`container` , `int`) --->  `map`
  *  **`distribution_of`** (`container`, `int`, `float`, `float`) --->  `map` 

#### Result: 
Discretize a list of values into n bins (computes the bins from a numerical variable into n (default 10) bins. Returns a distribution map with the values (values key), the interval legends (legend key), the distribution parameters (params keys, for cumulative charts). Parameters can be (list), (list, nbbins) or (list,nbbins,valmin,valmax)

#### Examples: 
```
 
map var0 <- distribution_of([1,1,2,12.5],10); // var0 equals map(['values'::[2,1,0,0,0,0,1,0,0,0],'legend'::['[0.0:2.0]','[2.0:4.0]','[4.0:6.0]','[6.0:8.0]','[8.0:10.0]','[10.0:12.0]','[12.0:14.0]','[14.0:16.0]','[16.0:18.0]','[18.0:20.0]'],'parlist'::[1,0]]) 
map var1 <- distribution_of([1,1,2,12.5]); // var1 equals map(['values'::[2,1,0,0,0,0,1,0,0,0],'legend'::['[0.0:2.0]','[2.0:4.0]','[4.0:6.0]','[6.0:8.0]','[8.0:10.0]','[10.0:12.0]','[12.0:14.0]','[14.0:16.0]','[16.0:18.0]','[18.0:20.0]'],'parlist'::[1,0]]) 
map var2 <- distribution_of([1,1,2,12.5]); // var2 equals map(['values'::[2,1,0,0,0,0,1,0,0,0],'legend'::['[0.0:2.0]','[2.0:4.0]','[4.0:6.0]','[6.0:8.0]','[8.0:10.0]','[10.0:12.0]','[12.0:14.0]','[14.0:16.0]','[16.0:18.0]','[18.0:20.0]'],'parlist'::[1,0]])

```
      


#### See also: 

[as_map](operators-a-to-a#as_map), 
    	
----

[//]: # (keyword|operator_distribution2d_of)
### `distribution2d_of`

#### Possible use: 
  * `container` **`distribution2d_of`** `container` --->  `map`
  *  **`distribution2d_of`** (`container` , `container`) --->  `map`
  *  **`distribution2d_of`** (`container`, `container`, `int`, `int`) --->  `map`
  *  **`distribution2d_of`** (`container`, `container`, `int`, `float`, `float`, `int`, `float`, `float`) --->  `map` 

#### Result: 
Discretize two lists of values into n bins (computes the bins from a numerical variable into n (default 10) bins. Returns a distribution map with the values (values key), the interval legends (legend key), the distribution parameters (params keys, for cumulative charts). Parameters can be (list), (list, nbbins) or (list,nbbins,valmin,valmax)

#### Examples: 
```
 
map var0 <- distribution2d_of([1,1,2,12.5]); // var0 equals map(['values'::[2,1,0,0,0,0,1,0,0,0],'legend'::['[0.0:2.0]','[2.0:4.0]','[4.0:6.0]','[6.0:8.0]','[8.0:10.0]','[10.0:12.0]','[12.0:14.0]','[14.0:16.0]','[16.0:18.0]','[18.0:20.0]'],'parlist'::[1,0]]) 
map var1 <- distribution_of([1,1,2,12.5],10); // var1 equals map(['values'::[2,1,0,0,0,0,1,0,0,0],'legend'::['[0.0:2.0]','[2.0:4.0]','[4.0:6.0]','[6.0:8.0]','[8.0:10.0]','[10.0:12.0]','[12.0:14.0]','[14.0:16.0]','[16.0:18.0]','[18.0:20.0]'],'parlist'::[1,0]]) 
map var2 <- distribution_of([1,1,2,12.5],10); // var2 equals map(['values'::[2,1,0,0,0,0,1,0,0,0],'legend'::['[0.0:2.0]','[2.0:4.0]','[4.0:6.0]','[6.0:8.0]','[8.0:10.0]','[10.0:12.0]','[12.0:14.0]','[14.0:16.0]','[16.0:18.0]','[18.0:20.0]'],'parlist'::[1,0]])

```
      


#### See also: 

[as_map](operators-a-to-a#as_map), 
    	
----

[//]: # (keyword|operator_div)
### `div`

#### Possible use: 
  * `int` **`div`** `int` --->  `int`
  *  **`div`** (`int` , `int`) --->  `int`
  * `float` **`div`** `int` --->  `int`
  *  **`div`** (`float` , `int`) --->  `int`
  * `float` **`div`** `float` --->  `int`
  *  **`div`** (`float` , `float`) --->  `int`
  * `int` **`div`** `float` --->  `int`
  *  **`div`** (`int` , `float`) --->  `int` 

#### Result: 
Returns the truncation of the division of the left-hand operand by the right-hand operand.

#### Special cases:     
  * if the right-hand operand is equal to zero, raises an exception.    
  * if the right-hand operand is equal to zero, raises an exception.    
  * if the right-hand operand is equal to zero, raises an exception.

#### Examples: 
```
 
int var0 <- 40 div 3; // var0 equals 13 
int var1 <- 40.5 div 3; // var1 equals 13 
int var2 <- 40.1 div 4.5; // var2 equals 8 
int var3 <- 40 div 4.1; // var3 equals 9

```
      


#### See also: 

[mod](operators-i-to-m#mod), 
    	
----

[//]: # (keyword|operator_dnorm)
### `dnorm`
   Same signification as [normal_density](operators-n-to-r#normal_density)
    	
----

[//]: # (keyword|operator_dtw)
### `dtw`

#### Possible use: 
  * `list` **`dtw`** `list` --->  `float`
  *  **`dtw`** (`list` , `list`) --->  `float`
  *  **`dtw`** (`list`, `list`, `int`) --->  `float` 

#### Result: 
returns the dynamic time warping between the two series of value with Sakoe-Chiba band (radius: the window width of Sakoe-Chiba band)
returns the dynamic time warping between the two series of value

#### Examples: 
```
 
float var0 <- dtw([10.0,5.0,1.0, 3.0],[1.0,10.0,5.0,1.0], 2); // var0 equals 2.0 
float var1 <- dtw([10.0,5.0,1.0, 3.0],[1.0,10.0,5.0,1.0]); // var1 equals 2

```
  
    	
----

[//]: # (keyword|operator_durbin_watson)
### `durbin_watson`

#### Possible use: 
  *  **`durbin_watson`** (`container`) --->  `float` 

#### Result: 
Durbin-Watson computation
    	
----

[//]: # (keyword|operator_dxf_file)
### `dxf_file`

#### Possible use: 
  *  **`dxf_file`** (`string`) --->  `file` 

#### Result: 
Constructs a file of type dxf. Allowed extensions are limited to dxf
    	
----

[//]: # (keyword|operator_edge)
### `edge`

#### Possible use: 
  *  **`edge`** (`pair`) --->  `unknown`
  *  **`edge`** (`unknown`) --->  `unknown`
  * `unknown` **`edge`** `float` --->  `unknown`
  *  **`edge`** (`unknown` , `float`) --->  `unknown`
  * `pair` **`edge`** `float` --->  `unknown`
  *  **`edge`** (`pair` , `float`) --->  `unknown`
  * `unknown` **`edge`** `unknown` --->  `unknown`
  *  **`edge`** (`unknown` , `unknown`) --->  `unknown`
  *  **`edge`** (`unknown`, `unknown`, `unknown`) --->  `unknown`
  *  **`edge`** (`unknown`, `unknown`, `float`) --->  `unknown`
  *  **`edge`** (`pair`, `unknown`, `float`) --->  `unknown`
  *  **`edge`** (`unknown`, `unknown`, `unknown`, `float`) --->  `unknown`
    	
----

[//]: # (keyword|operator_edge_between)
### `edge_between`

#### Possible use: 
  * `graph` **`edge_between`** `pair` --->  `unknown`
  *  **`edge_between`** (`graph` , `pair`) --->  `unknown` 

#### Result: 
returns the edge linking two nodes

#### Examples: 
```
 
unknown var0 <- graphFromMap edge_between node1::node2; // var0 equals edge1

```
      


#### See also: 

[out_edges_of](operators-n-to-r#out_edges_of), [in_edges_of](operators-i-to-m#in_edges_of), 
    	
----

[//]: # (keyword|operator_edge_betweenness)
### `edge_betweenness`

#### Possible use: 
  *  **`edge_betweenness`** (`graph`) --->  `map` 

#### Result: 
returns a map containing for each edge (key), its betweenness centrality (value): number of shortest paths passing through each edge

#### Examples: 
```
graph graphEpidemio <- graph([]);  
map var1 <- edge_betweenness(graphEpidemio); // var1 equals the edge betweenness index of the graph

```
  
    	
----

[//]: # (keyword|operator_edges)
### `edges`

#### Possible use: 
  *  **`edges`** (`container`) --->  `container`
    	
----

[//]: # (keyword|operator_eigenvalues)
### `eigenvalues`

#### Possible use: 
  *  **`eigenvalues`** (`matrix`) --->  `list<float>` 

#### Result: 
The eigen values (matrix) of the given matrix

#### Examples: 
```
 
list<float> var0 <- eigenvalues(matrix([[5,-3],[6,-4]])); // var0 equals [2.0000000000000004,-0.9999999999999998]

```
  
    	
----

[//]: # (keyword|operator_electre_DM)
### `electre_DM`

#### Possible use: 
  *  **`electre_DM`** (`msi.gama.util.IList<java.util.List>`, `msi.gama.util.IList<java.util.Map<java.lang.String,java.lang.Object>>`, `float`) --->  `int` 

#### Result: 
The index of the best candidate according to a method based on the ELECTRE methods. The principle of the ELECTRE methods is to compare the possible candidates by pair. These methods analyses the possible outranking relation existing between two candidates. An candidate outranks another if this one is at least as good as the other one. The ELECTRE methods are based on two concepts: the concordance and the discordance. The concordance characterizes the fact that, for an outranking relation to be validated, a sufficient majority of criteria should be in favor of this assertion. The discordance characterizes the fact that, for an outranking relation to be validated, none of the criteria in the minority should oppose too strongly this assertion. These two conditions must be true for validating the outranking assertion. More information about the ELECTRE methods can be found in [http://www.springerlink.com/content/g367r44322876223/	Figueira,  J., Mousseau, V., Roy, B.: ELECTRE Methods. In: Figueira, J., Greco, S., and Ehrgott, M., (Eds.), Multiple Criteria Decision Analysis: State of the Art Surveys, Springer, New York, 133--162 (2005)]. The first operand is the list of candidates (a candidate is a list of criterion values); the second operand the list of criterion: A criterion is a map that contains fives elements: a name, a weight, a preference value (p), an indifference value (q) and a veto value (v). The preference value represents the threshold from which the difference between two criterion values allows to prefer one vector of values over another. The indifference value represents the threshold from which the difference between two criterion values is considered significant. The veto value represents the threshold from which the difference between two criterion values disqualifies the candidate that obtained the smaller value; the last operand is the fuzzy cut.

#### Special cases:     
  * returns -1 is the list of candidates is nil or empty

#### Examples: 
```
 
int var0 <- electre_DM([[1.0, 7.0],[4.0,2.0],[3.0, 3.0]], [["name"::"utility", "weight" :: 2.0,"p"::0.5, "q"::0.0, "s"::1.0, "maximize" :: true],["name"::"price", "weight" :: 1.0,"p"::0.5, "q"::0.0, "s"::1.0, "maximize" :: false]],0.7); // var0 equals 0

```
      


#### See also: 

[weighted_means_DM](operators-s-to-z#weighted_means_dm), [promethee_DM](operators-n-to-r#promethee_dm), [evidence_theory_DM](operators-d-to-h#evidence_theory_dm), 
    	
----

[//]: # (keyword|operator_ellipse)
### `ellipse`

#### Possible use: 
  * `float` **`ellipse`** `float` --->  `geometry`
  *  **`ellipse`** (`float` , `float`) --->  `geometry` 

#### Result: 
An ellipse geometry which x-radius is equal to the first operand and y-radius is equal to the second operand  

#### Comment: 
the center of the ellipse is by default the location of the current agent in which has been called this operator.

#### Special cases:     
  * returns a point if both operands are lower or equal to 0, a line if only one is.

#### Examples: 
```
 
geometry var0 <- ellipse(10, 10); // var0 equals a geometry as an ellipse of width 10 and height 10.

```
      


#### See also: 

[around](operators-a-to-a#around), [cone](operators-b-to-c#cone), [line](operators-i-to-m#line), [link](operators-i-to-m#link), [norm](operators-n-to-r#norm), [point](operators-n-to-r#point), [polygon](operators-n-to-r#polygon), [polyline](operators-n-to-r#polyline), [rectangle](operators-n-to-r#rectangle), [square](operators-s-to-z#square), [circle](operators-b-to-c#circle), [squircle](operators-s-to-z#squircle), [triangle](operators-s-to-z#triangle), 
    	
----

[//]: # (keyword|operator_emotion)
### `emotion`

#### Possible use: 
  *  **`emotion`** (`any`) --->  `emotion` 

#### Result: 
Casts the operand into the type emotion
    	
----

[//]: # (keyword|operator_empty)
### `empty`

#### Possible use: 
  *  **`empty`** (`string`) --->  `bool`
  *  **`empty`** (`container<KeyType,ValueType>`) --->  `bool` 

#### Result: 
true if the operand is empty, false otherwise.  

#### Comment: 
the empty operator behavior depends on the nature of the operand

#### Special cases:     
  * if it is a map, empty returns true if the map contains no key-value mappings, and false otherwise    
  * if it is a file, empty returns true if the content of the file (that is also a container) is empty, and false otherwise    
  * if it is a population, empty returns true if there is no agent in the population, and false otherwise    
  * if it is a graph, empty returns true if it contains no vertex and no edge, and false otherwise    
  * if it is a matrix of int, float or object, it will return true if all elements are respectively 0, 0.0 or null, and false otherwise    
  * if it is a matrix of geometry, it will return true if the matrix contains no cell, and false otherwise    
  * if it is a string, empty returns true if the string does not contain any character, and false otherwise 
  
```
 
bool var0 <- empty ('abced'); // var0 equals false
``` 

    
  * if it is a list, empty returns true if there is no element in the list, and false otherwise 
  
```
 
bool var1 <- empty([]); // var1 equals true
``` 


    	
----

[//]: # (keyword|operator_enlarged_by)
### `enlarged_by`
   Same signification as [+](operators-a-to-a#+)
    	
----

[//]: # (keyword|operator_envelope)
### `envelope`

#### Possible use: 
  *  **`envelope`** (`unknown`) --->  `geometry` 

#### Result: 
A 3D geometry that represents the box that surrounds the geometries or the surface described by the arguments. More general than geometry(arguments).envelope, as it allows to pass int, double, point, image files, shape files, asc files, or any list combining these arguments, in which case the envelope will be correctly expanded. If an envelope cannot be determined from the arguments, a default one of dimensions (0,100, 0, 100, 0, 100) is returned
    	
----

[//]: # (keyword|operator_eval_gaml)
### `eval_gaml`

#### Possible use: 
  *  **`eval_gaml`** (`string`) --->  `unknown` 

#### Result: 
evaluates the given GAML string.

#### Examples: 
```
 
unknown var0 <- eval_gaml("2+3"); // var0 equals 5

```
  
    	
----

[//]: # (keyword|operator_eval_when)
### `eval_when`

#### Possible use: 
  *  **`eval_when`** (`BDIPlan`) --->  `bool` 

#### Result: 
evaluate the facet when of a given plan

#### Examples: 
```
eval_when(plan1) 

```
  
    	
----

[//]: # (keyword|operator_evaluate_sub_model)
### `evaluate_sub_model`

#### Possible use: 
  * `msi.gama.kernel.experiment.IExperimentAgent` **`evaluate_sub_model`** `string` --->  `unknown`
  *  **`evaluate_sub_model`** (`msi.gama.kernel.experiment.IExperimentAgent` , `string`) --->  `unknown` 

#### Result: 
Load a submodel  

#### Comment: 
loaded submodel
    	
----

[//]: # (keyword|operator_even)
### `even`

#### Possible use: 
  *  **`even`** (`int`) --->  `bool` 

#### Result: 
Returns true if the operand is even and false if it is odd.

#### Special cases:     
  * if the operand is equal to 0, it returns true.    
  * if the operand is a float, it is truncated before

#### Examples: 
```
 
bool var0 <- even (3); // var0 equals false 
bool var1 <- even(-12); // var1 equals true

```
  
    	
----

[//]: # (keyword|operator_every)
### `every`

#### Possible use: 
  *  **`every`** (`int`) --->  `bool`
  *  **`every`** (`any expression`) --->  `bool`
  * `msi.gama.util.GamaDateInterval` **`every`** `any expression` --->  `msi.gama.util.IList<msi.gama.util.GamaDate>`
  *  **`every`** (`msi.gama.util.GamaDateInterval` , `any expression`) --->  `msi.gama.util.IList<msi.gama.util.GamaDate>`
  * `list` **`every`** `int` --->  `list`
  *  **`every`** (`list` , `int`) --->  `list` 

#### Result: 
true every operand * cycle, false otherwise
applies a step to an interval of dates defined by 'date1 to date2'
Retrieves elements from the first argument every `step` (second argument) elements. Raises an error if the step is negative or equal to zero
expects a frequency (expressed in seconds of simulated time) as argument. Will return true every time the current_date matches with this frequency  

#### Comment: 
the value of the every operator depends on the cycle. It can be used to do something every x cycle.Used to do something at regular intervals of time. Can be used in conjunction with 'since', 'after', 'before', 'until' or 'between', so that this computation only takes place in the temporal segment defined by these operators. In all cases, the starting_date of the model is used as a reference starting point

#### Examples: 
```
if every(2#cycle) {write "the cycle number is even";} 	     else {write "the cycle number is odd";} (date('2000-01-01') to date('2010-01-01')) every (#month) // builds an interval between these two dates which contains all the monthly dates starting from the beginning of the interval reflex when: every(2#days) since date('2000-01-01') { .. } state a { transition to: b when: every(2#mn);} state b { transition to: a when: every(30#s);} // This oscillatory behavior will use the starting_date of the model as its starting point in time 

```
      


#### See also: 

[to](operators-s-to-z#to), [since](operators-s-to-z#since), [after](operators-a-to-a#after), 
    	
----

[//]: # (keyword|operator_every_cycle)
### `every_cycle`
   Same signification as [every](operators-d-to-h#every)
    	
----

[//]: # (keyword|operator_evidence_theory_DM)
### `evidence_theory_DM`

#### Possible use: 
  * `msi.gama.util.IList<java.util.List>` **`evidence_theory_DM`** `msi.gama.util.IList<java.util.Map<java.lang.String,java.lang.Object>>` --->  `int`
  *  **`evidence_theory_DM`** (`msi.gama.util.IList<java.util.List>` , `msi.gama.util.IList<java.util.Map<java.lang.String,java.lang.Object>>`) --->  `int`
  *  **`evidence_theory_DM`** (`msi.gama.util.IList<java.util.List>`, `msi.gama.util.IList<java.util.Map<java.lang.String,java.lang.Object>>`, `bool`) --->  `int` 

#### Result: 
The index of the best candidate according to a method based on the Evidence theory. This theory, which was proposed by Shafer ([http://www.glennshafer.com/books/amte.html Shafer G (1976) A mathematical theory of evidence, Princeton University Press]), is based on the work of Dempster ([http://projecteuclid.org/DPubS?service=UI&version=1.0&verb=Display&handle=euclid.aoms/1177698950 Dempster A (1967) Upper and lower probabilities induced by multivalued mapping. Annals of Mathematical Statistics, vol.  38, pp. 325--339]) on lower and upper probability distributions. The first operand is the list of candidates (a candidate is a list of criterion values); the second operand the list of criterion: A criterion is a map that contains seven elements: a name, a first threshold s1, a second threshold s2, a value for the assertion "this candidate is the best" at threshold s1 (v1p), a value for the assertion "this candidate is the best" at threshold s2 (v2p), a value for the assertion "this candidate is not the best" at threshold s1 (v1c), a value for the assertion "this candidate is not the best" at threshold s2 (v2c). v1p, v2p, v1c and v2c have to been defined in order that: v1p + v1c <= 1.0; v2p + v2c <= 1.0.; the last operand allows to use a simple version of this multi-criteria decision making method (simple if true)

#### Special cases:     
  * returns -1 is the list of candidates is nil or empty    
  * if the operator is used with only 2 operands (the candidates and the criteria), the last parameter (use simple method) is set to true

#### Examples: 
```
 
int var0 <- evidence_theory_DM([[1.0, 7.0],[4.0,2.0],[3.0, 3.0]], [["name"::"utility", "s1" :: 0.0,"s2"::1.0, "v1p"::0.0, "v2p"::1.0, "v1c"::0.0, "v2c"::0.0, "maximize" :: true],["name"::"price",  "s1" :: 0.0,"s2"::1.0, "v1p"::0.0, "v2p"::1.0, "v1c"::0.0, "v2c"::0.0, "maximize" :: true]], true); // var0 equals 0

```
      


#### See also: 

[weighted_means_DM](operators-s-to-z#weighted_means_dm), [electre_DM](operators-d-to-h#electre_dm), 
    	
----

[//]: # (keyword|operator_exp)
### `exp`

#### Possible use: 
  *  **`exp`** (`float`) --->  `float`
  *  **`exp`** (`int`) --->  `float` 

#### Result: 
Returns Euler's number e raised to the power of the operand.

#### Special cases:     
  * the operand is casted to a float before being evaluated.    
  * the operand is casted to a float before being evaluated.

#### Examples: 
```
 
float var0 <- exp (0); // var0 equals 1.0

```
      


#### See also: 

[ln](operators-i-to-m#ln), 
    	
----

[//]: # (keyword|operator_fact)
### `fact`

#### Possible use: 
  *  **`fact`** (`int`) --->  `float` 

#### Result: 
Returns the factorial of the operand.

#### Special cases:     
  * if the operand is less than 0, fact returns 0.

#### Examples: 
```
 
float var0 <- fact(4); // var0 equals 24

```
  
    	
----

[//]: # (keyword|operator_farthest_point_to)
### `farthest_point_to`

#### Possible use: 
  * `geometry` **`farthest_point_to`** `point` --->  `point`
  *  **`farthest_point_to`** (`geometry` , `point`) --->  `point` 

#### Result: 
the farthest point of the left-operand to the left-point.

#### Examples: 
```
 
point var0 <- geom farthest_point_to(pt); // var0 equals the farthest point of geom to pt

```
      


#### See also: 

[any_location_in](operators-a-to-a#any_location_in), [any_point_in](operators-a-to-a#any_point_in), [closest_points_with](operators-b-to-c#closest_points_with), [points_at](operators-n-to-r#points_at), 
    	
----

[//]: # (keyword|operator_farthest_to)
### `farthest_to`

#### Possible use: 
  * `container<agent>` **`farthest_to`** `geometry` --->  `geometry`
  *  **`farthest_to`** (`container<agent>` , `geometry`) --->  `geometry` 

#### Result: 
An agent or a geometry among the left-operand list of agents, species or meta-population (addition of species), the farthest to the operand (casted as a geometry).  

#### Comment: 
the distance is computed in the topology of the calling agent (the agent in which this operator is used), with the distance algorithm specific to the topology.

#### Examples: 
```
 
geometry var0 <- [ag1, ag2, ag3] closest_to(self); // var0 equals return the farthest agent among ag1, ag2 and ag3 to the agent applying the operator.(species1 + species2) closest_to self 

```
      


#### See also: 

[neighbors_at](operators-n-to-r#neighbors_at), [neighbors_of](operators-n-to-r#neighbors_of), [inside](operators-i-to-m#inside), [overlapping](operators-n-to-r#overlapping), [agents_overlapping](operators-a-to-a#agents_overlapping), [agents_inside](operators-a-to-a#agents_inside), [agent_closest_to](operators-a-to-a#agent_closest_to), [closest_to](operators-b-to-c#closest_to), [agent_farthest_to](operators-a-to-a#agent_farthest_to), 
    	
----

[//]: # (keyword|operator_file)
### `file`

#### Possible use: 
  *  **`file`** (`string`) --->  `file`
  * `string` **`file`** `container` --->  `file`
  *  **`file`** (`string` , `container`) --->  `file` 

#### Result: 
opens a file in read only mode, creates a GAML file object, and tries to determine and store the file content in the contents attribute.
Creates a file in read/write mode, setting its contents to the container passed in parameter  

#### Comment: 
The file should have a supported extension, see file type definition for supported file extensions.The type of container to pass will depend on the type of file (see the management of files in the documentation). Can be used to copy files since files are considered as containers. For example: save file('image_copy.png', file('image.png')); will copy image.png to image_copy.png

#### Special cases:     
  * If the specified string does not refer to an existing file, an exception is risen when the variable is used.

#### Examples: 
```
let fileT type: file value: file("../includes/Stupid_Cell.Data");  			// fileT represents the file "../includes/Stupid_Cell.Data" 			// fileT.contents here contains a matrix storing all the data of the text file 

```
      


#### See also: 

[folder](operators-d-to-h#folder), [new_folder](operators-n-to-r#new_folder), 
    	
----

[//]: # (keyword|operator_file)
### `file`

#### Possible use: 
  *  **`file`** (`any`) --->  `file` 

#### Result: 
Casts the operand into the type file
    	
----

[//]: # (keyword|operator_file_exists)
### `file_exists`

#### Possible use: 
  *  **`file_exists`** (`string`) --->  `bool` 

#### Result: 
Test whether the parameter is the path to an existing file.
    	
----

[//]: # (keyword|operator_first)
### `first`

#### Possible use: 
  *  **`first`** (`container<KeyType,ValueType>`) --->  `ValueType`
  *  **`first`** (`string`) --->  `string`
  * `int` **`first`** `container` --->  `list`
  *  **`first`** (`int` , `container`) --->  `list` 

#### Result: 
the first value of the operand  

#### Comment: 
the first operator behavior depends on the nature of the operand

#### Special cases:     
  * if it is a map, first returns the first value of the first pair (in insertion order)    
  * if it is a file, first returns the first element of the content of the file (that is also a container)    
  * if it is a population, first returns the first agent of the population    
  * if it is a graph, first returns the first edge (in creation order)    
  * if it is a matrix, first returns the element at {0,0} in the matrix    
  * for a matrix of int or float, it will return 0 if the matrix is empty    
  * for a matrix of object or geometry, it will return nil if the matrix is empty    
  * if it is a list, first returns the first element of the list, or nil if the list is empty 
  
```
 
int var0 <- first ([1, 2, 3]); // var0 equals 1
``` 

    
  * if it is a string, first returns a string composed of its first character 
  
```
 
string var1 <- first ('abce'); // var1 equals 'a'
``` 

    


#### See also: 

[last](operators-i-to-m#last), 
    	
----

[//]: # (keyword|operator_first_of)
### `first_of`
   Same signification as [first](operators-d-to-h#first)
    	
----

[//]: # (keyword|operator_first_with)
### `first_with`

#### Possible use: 
  * `container` **`first_with`** `any expression` --->  `unknown`
  *  **`first_with`** (`container` , `any expression`) --->  `unknown` 

#### Result: 
the first element of the left-hand operand that makes the right-hand operand evaluate to true.  

#### Comment: 
in the right-hand operand, the keyword each can be used to represent, in turn, each of the right-hand operand elements.

#### Special cases:     
  * if the left-hand operand is nil, first_with throws an error. If there is no element that satisfies the condition, it returns nil    
  * if the left-operand is a map, the keyword each will contain each value 
  
```
 
unknown var4 <- [1::2, 3::4, 5::6] first_with (each >= 4); // var4 equals 4 
unknown var5 <- [1::2, 3::4, 5::6].pairs first_with (each.value >= 4); // var5 equals (3::4)
``` 



#### Examples: 
```
 
unknown var0 <- [1,2,3,4,5,6,7,8] first_with (each > 3); // var0 equals 4 
unknown var2 <- g2 first_with (length(g2 out_edges_of each) = 0); // var2 equals node9 
unknown var3 <- (list(node) first_with (round(node(each).location.x) > 32); // var3 equals node2

```
      


#### See also: 

[group_by](operators-d-to-h#group_by), [last_with](operators-i-to-m#last_with), [where](operators-s-to-z#where), 
    	
----

[//]: # (keyword|operator_flip)
### `flip`

#### Possible use: 
  *  **`flip`** (`float`) --->  `bool` 

#### Result: 
true or false given the probability represented by the operand

#### Special cases:     
  * flip 0 always returns false, flip 1 true

#### Examples: 
```
 
bool var0 <- flip (0.66666); // var0 equals 2/3 chances to return true.

```
      


#### See also: 

[rnd](operators-n-to-r#rnd), 
    	
----

[//]: # (keyword|operator_float)
### `float`

#### Possible use: 
  *  **`float`** (`any`) --->  `float` 

#### Result: 
Casts the operand into the type float
    	
----

[//]: # (keyword|operator_floor)
### `floor`

#### Possible use: 
  *  **`floor`** (`float`) --->  `float` 

#### Result: 
Maps the operand to the largest previous following integer, i.e. the largest integer not greater than x.

#### Examples: 
```
 
float var0 <- floor(3); // var0 equals 3.0 
float var1 <- floor(3.5); // var1 equals 3.0 
float var2 <- floor(-4.7); // var2 equals -5.0

```
      


#### See also: 

[ceil](operators-b-to-c#ceil), [round](operators-n-to-r#round), 
    	
----

[//]: # (keyword|operator_folder)
### `folder`

#### Possible use: 
  *  **`folder`** (`string`) --->  `file` 

#### Result: 
opens an existing repository

#### Special cases:     
  * If the specified string does not refer to an existing repository, an exception is risen.

#### Examples: 
```
file dirT <- folder("../includes/"); 				// dirT represents the repository "../includes/" 				// dirT.contents here contains the list of the names of included files 

```
      


#### See also: 

[file](operators-d-to-h#file), [new_folder](operators-n-to-r#new_folder), 
    	
----

[//]: # (keyword|operator_font)
### `font`

#### Possible use: 
  *  **`font`** (`string`, `int`, `int`) --->  `font` 

#### Result: 
Creates a new font, by specifying its name (either a font face name like 'Lucida Grande Bold' or 'Helvetica', or a logical name like 'Dialog', 'SansSerif', 'Serif', etc.), a size in points and a style, either #bold, #italic or #plain or a combination (addition) of them.

#### Examples: 
```
 
font var0 <- font ('Helvetica Neue',12, #bold + #italic); // var0 equals a bold and italic face of the Helvetica Neue family

```
  
    	
----

[//]: # (keyword|operator_frequency_of)
### `frequency_of`

#### Possible use: 
  * `container` **`frequency_of`** `any expression` --->  `map`
  *  **`frequency_of`** (`container` , `any expression`) --->  `map` 

#### Result: 
Returns a map with keys equal to the application of the right-hand argument (like collect) and values equal to the frequency of this key (i.e. how many times it has been obtained)

#### Examples: 
```
 
map var0 <- [ag1, ag2, ag3, ag4] frequency_of each.size; // var0 equals the different sizes as keys and the number of agents of this size as values

```
      


#### See also: 

[as_map](operators-a-to-a#as_map), 
    	
----

[//]: # (keyword|operator_from)
### `from`
   Same signification as [since](operators-s-to-z#since)
    	
----

[//]: # (keyword|operator_fuzzy_choquet_DM)
### `fuzzy_choquet_DM`

#### Possible use: 
  *  **`fuzzy_choquet_DM`** (`msi.gama.util.IList<java.util.List>`, `list<string>`, `map`) --->  `int` 

#### Result: 
The index of the candidate that maximizes the Fuzzy Choquet Integral value. The first operand is the list of candidates (a candidate is a list of criterion values); the second operand the list of criterion (list of string); the third operand the weights of each sub-set of criteria (map with list for key and float for value)

#### Special cases:     
  * returns -1 is the list of candidates is nil or empty

#### Examples: 
```
 
int var0 <- fuzzy_choquet_DM([[1.0, 7.0],[4.0,2.0],[3.0, 3.0]], ["utility", "price", "size"],[["utility"]::0.5,["size"]::0.1,["price"]::0.4,["utility", "price"]::0.55]); // var0 equals 0

```
      


#### See also: 

[promethee_DM](operators-n-to-r#promethee_dm), [electre_DM](operators-d-to-h#electre_dm), [evidence_theory_DM](operators-d-to-h#evidence_theory_dm), 
    	
----

[//]: # (keyword|operator_fuzzy_kappa)
### `fuzzy_kappa`

#### Possible use: 
  *  **`fuzzy_kappa`** (`list<agent>`, `list`, `list`, `list<float>`, `list`, `matrix<float>`, `float`) --->  `float`
  *  **`fuzzy_kappa`** (`list<agent>`, `list`, `list`, `list<float>`, `list`, `matrix<float>`, `float`, `list`) --->  `float` 

#### Result: 
fuzzy kappa indicator for 2 map comparisons: fuzzy_kappa(agents_list,list_vals1,list_vals2, output_similarity_per_agents,categories,fuzzy_categories_matrix, fuzzy_distance, weights). Reference: Visser, H., and T. de Nijs, 2006. The map comparison kit, Environmental Modelling & Software, 21
fuzzy kappa indicator for 2 map comparisons: fuzzy_kappa(agents_list,list_vals1,list_vals2, output_similarity_per_agents,categories,fuzzy_categories_matrix, fuzzy_distance). Reference: Visser, H., and T. de Nijs, 2006. The map comparison kit, Environmental Modelling & Software, 21

#### Examples: 
```
fuzzy_kappa([ag1, ag2, ag3, ag4, ag5],[cat1,cat1,cat2,cat3,cat2],[cat2,cat1,cat2,cat1,cat2], similarity_per_agents,[cat1,cat2,cat3],[[1,0,0],[0,1,0],[0,0,1]], 2, [1.0,3.0,2.0,2.0,4.0]) fuzzy_kappa([ag1, ag2, ag3, ag4, ag5],[cat1,cat1,cat2,cat3,cat2],[cat2,cat1,cat2,cat1,cat2], similarity_per_agents,[cat1,cat2,cat3],[[1,0,0],[0,1,0],[0,0,1]], 2) 

```
  
    	
----

[//]: # (keyword|operator_fuzzy_kappa_sim)
### `fuzzy_kappa_sim`

#### Possible use: 
  *  **`fuzzy_kappa_sim`** (`list<agent>`, `list`, `list`, `list`, `list<float>`, `list`, `matrix<float>`, `float`) --->  `float`
  *  **`fuzzy_kappa_sim`** (`list<agent>`, `list`, `list`, `list`, `list<float>`, `list`, `matrix<float>`, `float`, `list`) --->  `float` 

#### Result: 
fuzzy kappa simulation indicator for 2 map comparisons: fuzzy_kappa_sim(agents_list,list_vals1,list_vals2, output_similarity_per_agents,fuzzy_transitions_matrix, fuzzy_distance, weights). Reference: Jasper van Vliet, Alex Hagen-Zanker, Jelle Hurkens, Hedwig van Delden, A fuzzy set approach to assess the predictive accuracy of land use simulations, Ecological Modelling, 24 July 2013, Pages 32-42, ISSN 0304-3800, 
fuzzy kappa simulation indicator for 2 map comparisons: fuzzy_kappa_sim(agents_list,list_vals1,list_vals2, output_similarity_per_agents,fuzzy_transitions_matrix, fuzzy_distance). Reference: Jasper van Vliet, Alex Hagen-Zanker, Jelle Hurkens, Hedwig van Delden, A fuzzy set approach to assess the predictive accuracy of land use simulations, Ecological Modelling, 24 July 2013, Pages 32-42, ISSN 0304-3800,

#### Examples: 
```
fuzzy_kappa_sim([ag1, ag2, ag3, ag4, ag5], [cat1,cat1,cat2,cat3,cat2],[cat2,cat1,cat2,cat1,cat2], similarity_per_agents,[cat1,cat2,cat3],[[1,0,0,0,0,0,0,0,0],[0,1,0,0,0,0,0,0,0],[0,0,1,0,0,0,0,0,0],[0,0,0,1,0,0,0,0,0],[0,0,0,0,1,0,0,0,0],[0,0,0,0,0,1,0,0,0],[0,0,0,0,0,0,1,0,0],[0,0,0,0,0,0,0,1,0],[0,0,0,0,0,0,0,0,1]], 2,[1.0,3.0,2.0,2.0,4.0]) fuzzy_kappa_sim([ag1, ag2, ag3, ag4, ag5], [cat1,cat1,cat2,cat3,cat2],[cat2,cat1,cat2,cat1,cat2], similarity_per_agents,[cat1,cat2,cat3],[[1,0,0,0,0,0,0,0,0],[0,1,0,0,0,0,0,0,0],[0,0,1,0,0,0,0,0,0],[0,0,0,1,0,0,0,0,0],[0,0,0,0,1,0,0,0,0],[0,0,0,0,0,1,0,0,0],[0,0,0,0,0,0,1,0,0],[0,0,0,0,0,0,0,1,0],[0,0,0,0,0,0,0,0,1]], 2) 

```
  
    	
----

[//]: # (keyword|operator_gaml_file)
### `gaml_file`

#### Possible use: 
  *  **`gaml_file`** (`string`) --->  `file` 

#### Result: 
Constructs a file of type gaml. Allowed extensions are limited to gaml, experiment
    	
----

[//]: # (keyword|operator_gaml_type)
### `gaml_type`

#### Possible use: 
  *  **`gaml_type`** (`any`) --->  `gaml_type` 

#### Result: 
Casts the operand into the type gaml_type
    	
----

[//]: # (keyword|operator_gamma)
### `gamma`

#### Possible use: 
  *  **`gamma`** (`float`) --->  `float` 

#### Result: 
Returns the value of the Gamma function at x.
    	
----

[//]: # (keyword|operator_gamma_distribution)
### `gamma_distribution`

#### Possible use: 
  *  **`gamma_distribution`** (`float`, `float`, `float`) --->  `float` 

#### Result: 
Returns the integral from zero to x of the gamma probability density function.  

#### Comment: 
incomplete_gamma(a,x) is equal to pgamma(a,1,x).
    	
----

[//]: # (keyword|operator_gamma_distribution_complemented)
### `gamma_distribution_complemented`

#### Possible use: 
  *  **`gamma_distribution_complemented`** (`float`, `float`, `float`) --->  `float` 

#### Result: 
Returns the integral from x to infinity of the gamma probability density function.
    	
----

[//]: # (keyword|operator_gamma_index)
### `gamma_index`

#### Possible use: 
  *  **`gamma_index`** (`graph`) --->  `float` 

#### Result: 
returns the gamma index of the graph (A measure of connectivity that considers the relationship between the number of observed links and the number of possible links: gamma = e/(3 `*` (v - 2)) - for planar graph.

#### Examples: 
```
graph graphEpidemio <- graph([]);  
float var1 <- gamma_index(graphEpidemio); // var1 equals the gamma index of the graph

```
      


#### See also: 

[alpha_index](operators-a-to-a#alpha_index), [beta_index](operators-b-to-c#beta_index), [nb_cycles](operators-n-to-r#nb_cycles), [connectivity_index](operators-b-to-c#connectivity_index), 
    	
----

[//]: # (keyword|operator_gamma_rnd)
### `gamma_rnd`

#### Possible use: 
  * `float` **`gamma_rnd`** `float` --->  `float`
  *  **`gamma_rnd`** (`float` , `float`) --->  `float` 

#### Result: 
returns a random value from a gamma distribution with specified values of the shape and scale parameters

#### Examples: 
```
gamma_rnd(10.0,5.0) 

```
  
    	
----

[//]: # (keyword|operator_gauss)
### `gauss`

#### Possible use: 
  *  **`gauss`** (`point`) --->  `float`
  * `float` **`gauss`** `float` --->  `float`
  *  **`gauss`** (`float` , `float`) --->  `float` 

#### Result: 
A value from a normally distributed random variable with expected value (mean as first operand) and variance (standardDeviation as second operand). The probability density function of such a variable is a Gaussian.
The operator can be used with an operand of type point {meand,standardDeviation}.

#### Special cases:     
  * when standardDeviation value is 0.0, it always returns the mean value    
  * when the operand is a point, it is read as {mean, standardDeviation}

#### Examples: 
```
 
float var0 <- gauss(0,0.3); // var0 equals 0.22354 
float var1 <- gauss({0,0.3}); // var1 equals 0.22354

```
      


#### See also: 

[skew_gauss](operators-s-to-z#skew_gauss), [truncated_gauss](operators-s-to-z#truncated_gauss), [poisson](operators-n-to-r#poisson), 
    	
----

[//]: # (keyword|operator_generate_barabasi_albert)
### `generate_barabasi_albert`

#### Possible use: 
  *  **`generate_barabasi_albert`** (`container<agent>`, `species`, `int`, `bool`) --->  `graph`
  *  **`generate_barabasi_albert`** (`species`, `species`, `int`, `int`, `bool`) --->  `graph` 

#### Result: 
returns a random scale-free network (following Barabasi-Albert (BA) model).
returns a random scale-free network (following Barabasi-Albert (BA) model).  

#### Comment: 
The Barabasi-Albert (BA) model is an algorithm for generating random scale-free networks using a preferential attachment mechanism. A scale-free network is a network whose degree distribution follows a power law, at least asymptotically.Such networks are widely observed in natural and human-made systems, including the Internet, the world wide web, citation networks, and some social networks. [From Wikipedia article]The map operand should includes following elements:The Barabasi-Albert (BA) model is an algorithm for generating random scale-free networks using a preferential attachment mechanism. A scale-free network is a network whose degree distribution follows a power law, at least asymptotically.Such networks are widely observed in natural and human-made systems, including the Internet, the world wide web, citation networks, and some social networks. [From Wikipedia article]The map operand should includes following elements:

#### Special cases:     
  * "vertices_specy": the species of vertices    
  * "edges_species": the species of edges    
  * "size": the graph will contain (size + 1) nodes    
  * "m": the number of edges added per novel node    
  * "synchronized": is the graph and the species of vertices and edges synchronized?    
  * "agents": list of existing node agents    
  * "edges_species": the species of edges    
  * "size": the graph will contain (size + 1) nodes    
  * "m": the number of edges added per novel node    
  * "synchronized": is the graph and the species of vertices and edges synchronized?

#### Examples: 
```
graph<yourNodeSpecy,yourEdgeSpecy> graphEpidemio <- generate_barabasi_albert( 		yourNodeSpecy, 		yourEdgeSpecy, 		3, 		5, 		true); graph<yourNodeSpecy,yourEdgeSpecy> graphEpidemio <- generate_barabasi_albert( 		yourListOfNodes, 		yourEdgeSpecy, 		3, 		5, 		true); 

```
      


#### See also: 

[generate_watts_strogatz](operators-d-to-h#generate_watts_strogatz), 
    	
----

[//]: # (keyword|operator_generate_complete_graph)
### `generate_complete_graph`

#### Possible use: 
  *  **`generate_complete_graph`** (`container<agent>`, `species`, `bool`) --->  `graph`
  *  **`generate_complete_graph`** (`container<agent>`, `species`, `float`, `bool`) --->  `graph`
  *  **`generate_complete_graph`** (`species`, `species`, `int`, `bool`) --->  `graph`
  *  **`generate_complete_graph`** (`species`, `species`, `int`, `float`, `bool`) --->  `graph` 

#### Result: 
returns a fully connected graph.
returns a fully connected graph.
returns a fully connected graph.
returns a fully connected graph.  

#### Comment: 
Arguments should include following elements:Arguments should include following elements:Arguments should include following elements:Arguments should include following elements:

#### Special cases:     
  * "vertices_specy": the species of vertices    
  * "edges_species": the species of edges    
  * "size": the graph will contain size nodes.    
  * "layoutRadius": nodes of the graph will be located on a circle with radius layoutRadius and centered in the environment.    
  * "synchronized": is the graph and the species of vertices and edges synchronized?    
  * "agents": list of existing node agents    
  * "edges_species": the species of edges    
  * "layoutRadius": nodes of the graph will be located on a circle with radius layoutRadius and centered in the environment.    
  * "synchronized": is the graph and the species of vertices and edges synchronized?    
  * "vertices_specy": the species of vertices    
  * "edges_species": the species of edges    
  * "size": the graph will contain size nodes.    
  * "synchronized": is the graph and the species of vertices and edges synchronized?    
  * "agents": list of existing node agents    
  * "edges_species": the species of edges    
  * "synchronized": is the graph and the species of vertices and edges synchronized?

#### Examples: 
```
graph<myVertexSpecy,myEdgeSpecy> myGraph <- generate_complete_graph( 			myVertexSpecy, 			myEdgeSpecy, 			10, 25, 		true); graph<myVertexSpecy,myEdgeSpecy> myGraph <- generate_complete_graph( 			myListOfNodes, 			myEdgeSpecy, 			25, 		true); graph<myVertexSpecy,myEdgeSpecy> myGraph <- generate_complete_graph( 			myVertexSpecy, 			myEdgeSpecy, 			10, 		true); graph<myVertexSpecy,myEdgeSpecy> myGraph <- generate_complete_graph( 			myListOfNodes, 			myEdgeSpecy, 		true); 

```
      


#### See also: 

[generate_barabasi_albert](operators-d-to-h#generate_barabasi_albert), [generate_watts_strogatz](operators-d-to-h#generate_watts_strogatz), 
    	
----

[//]: # (keyword|operator_generate_watts_strogatz)
### `generate_watts_strogatz`

#### Possible use: 
  *  **`generate_watts_strogatz`** (`container<agent>`, `species`, `float`, `int`, `bool`) --->  `graph`
  *  **`generate_watts_strogatz`** (`species`, `species`, `int`, `float`, `int`, `bool`) --->  `graph` 

#### Result: 
returns a random small-world network (following Watts-Strogatz model).
returns a random small-world network (following Watts-Strogatz model).  

#### Comment: 
The Watts-Strogatz model is a random graph generation model that produces graphs with small-world properties, including short average path lengths and high clustering.A small-world network is a type of graph in which most nodes are not neighbors of one another, but most nodes can be reached from every other by a small number of hops or steps. [From Wikipedia article]The map operand should includes following elements:The Watts-Strogatz model is a random graph generation model that produces graphs with small-world properties, including short average path lengths and high clustering.A small-world network is a type of graph in which most nodes are not neighbors of one another, but most nodes can be reached from every other by a small number of hops or steps. [From Wikipedia article]The map operand should includes following elements:

#### Special cases:     
  * "vertices_specy": the species of vertices    
  * "edges_species": the species of edges    
  * "size": the graph will contain (size + 1) nodes. Size must be greater than k.    
  * "p": probability to "rewire" an edge. So it must be between 0 and 1. The parameter is often called beta in the literature.    
  * "k": the base degree of each node. k must be greater than 2 and even.    
  * "synchronized": is the graph and the species of vertices and edges synchronized?    
  * "agents": list of existing node agents    
  * "edges_species": the species of edges    
  * "p": probability to "rewire" an edge. So it must be between 0 and 1. The parameter is often called beta in the literature.    
  * "k": the base degree of each node. k must be greater than 2 and even.    
  * "synchronized": is the graph and the species of vertices and edges synchronized?

#### Examples: 
```
graph<myVertexSpecy,myEdgeSpecy> myGraph <- generate_watts_strogatz( 			myVertexSpecy, 			myEdgeSpecy, 			2, 			0.3, 			2, 		true); graph<myVertexSpecy,myEdgeSpecy> myGraph <- generate_watts_strogatz( 			myListOfNodes, 			myEdgeSpecy, 			0.3, 			2, 		true); 

```
      


#### See also: 

[generate_barabasi_albert](operators-d-to-h#generate_barabasi_albert), 
    	
----

[//]: # (keyword|operator_geojson_file)
### `geojson_file`

#### Possible use: 
  *  **`geojson_file`** (`string`) --->  `file` 

#### Result: 
Constructs a file of type geojson. Allowed extensions are limited to json, geojson, geo.json
    	
----

[//]: # (keyword|operator_geometric_mean)
### `geometric_mean`

#### Possible use: 
  *  **`geometric_mean`** (`container`) --->  `float` 

#### Result: 
the geometric mean of the elements of the operand. See <A href="http://en.wikipedia.org/wiki/Geometric_mean">Geometric_mean</A> for more details.  

#### Comment: 
The operator casts all the numerical element of the list into float. The elements that are not numerical are discarded.

#### Examples: 
```
 
float var0 <- geometric_mean ([4.5, 3.5, 5.5, 7.0]); // var0 equals 4.962326343467649

```
      


#### See also: 

[mean](operators-i-to-m#mean), [median](operators-i-to-m#median), [harmonic_mean](operators-d-to-h#harmonic_mean), 
    	
----

[//]: # (keyword|operator_geometry)
### `geometry`

#### Possible use: 
  *  **`geometry`** (`any`) --->  `geometry` 

#### Result: 
Casts the operand into the type geometry
    	
----

[//]: # (keyword|operator_geometry_collection)
### `geometry_collection`

#### Possible use: 
  *  **`geometry_collection`** (`container<geometry>`) --->  `geometry` 

#### Result: 
A geometry collection (multi-geometry) composed of the given list of geometries.

#### Special cases:     
  * if the operand is nil, returns the point geometry {0,0}    
  * if the operand is composed of a single geometry, returns a copy of the geometry.

#### Examples: 
```
 
geometry var0 <- geometry_collection([{0,0}, {0,10}, {10,10}, {10,0}]); // var0 equals a geometry composed of the 4 points (multi-point).

```
      


#### See also: 

[around](operators-a-to-a#around), [circle](operators-b-to-c#circle), [cone](operators-b-to-c#cone), [link](operators-i-to-m#link), [norm](operators-n-to-r#norm), [point](operators-n-to-r#point), [polygone](operators-s-to-z#polygone), [rectangle](operators-n-to-r#rectangle), [square](operators-s-to-z#square), [triangle](operators-s-to-z#triangle), [line](operators-i-to-m#line), 
    	
----

[//]: # (keyword|operator_get)
### `get`

#### Possible use: 
  * `geometry` **`get`** `string` --->  `unknown`
  *  **`get`** (`geometry` , `string`) --->  `unknown`
  * `agent` **`get`** `string` --->  `unknown`
  *  **`get`** (`agent` , `string`) --->  `unknown` 

#### Result: 
Reads an attribute of the specified geometry (left operand). The attribute name is specified by the right operand.
Reads an attribute of the specified agent (left operand). The attribute name is specified by the right operand.

#### Special cases:     
  * Reading the attribute of a geometry 
  
```
string geom_area <- a_geometry get('area');     // reads then 'area' attribute of 'a_geometry' variable then assigns the returned value to the geom_area variable 
``` 

    
  * Reading the attribute of another agent 
  
```
string agent_name <- an_agent get('name');     // reads then 'name' attribute of an_agent then assigns the returned value to the agent_name variable 
``` 


    	
----

[//]: # (keyword|operator_get_about)
### `get_about`

#### Possible use: 
  *  **`get_about`** (`emotion`) --->  `predicate` 

#### Result: 
get the about value of the given emotion

#### Examples: 
```
get_about(emotion) 

```
  
    	
----

[//]: # (keyword|operator_get_agent)
### `get_agent`

#### Possible use: 
  *  **`get_agent`** (`msi.gaml.architecture.simplebdi.SocialLink`) --->  `agent` 

#### Result: 
get the agent value of the given social link

#### Examples: 
```
get_agent(social_link1) 

```
  
    	
----

[//]: # (keyword|operator_get_agent_cause)
### `get_agent_cause`

#### Possible use: 
  *  **`get_agent_cause`** (`emotion`) --->  `agent`
  *  **`get_agent_cause`** (`predicate`) --->  `agent` 

#### Result: 
get the agent cause value of the given emotion

#### Examples: 
```
get_agent_cause(emotion) 

```
  
    	
----

[//]: # (keyword|operator_get_belief_op)
### `get_belief_op`

#### Possible use: 
  * `agent` **`get_belief_op`** `predicate` --->  `mental_state`
  *  **`get_belief_op`** (`agent` , `predicate`) --->  `mental_state` 

#### Result: 
get the belief in the belief base with the given predicate.

#### Examples: 
```
get_belief_op(self,has_water) 

```
  
    	
----

[//]: # (keyword|operator_get_belief_with_name_op)
### `get_belief_with_name_op`

#### Possible use: 
  * `agent` **`get_belief_with_name_op`** `string` --->  `mental_state`
  *  **`get_belief_with_name_op`** (`agent` , `string`) --->  `mental_state` 

#### Result: 
get the belief in the belief base with the given name.

#### Examples: 
```
get_belief_with_name_op(self,"has_water") 

```
  
    	
----

[//]: # (keyword|operator_get_beliefs_op)
### `get_beliefs_op`

#### Possible use: 
  * `agent` **`get_beliefs_op`** `predicate` --->  `msi.gama.util.IList<msi.gaml.architecture.simplebdi.MentalState>`
  *  **`get_beliefs_op`** (`agent` , `predicate`) --->  `msi.gama.util.IList<msi.gaml.architecture.simplebdi.MentalState>` 

#### Result: 
get the beliefs in the belief base with the given predicate.

#### Examples: 
```
get_beliefs_op(self,has_water) 

```
  
    	
----

[//]: # (keyword|operator_get_beliefs_with_name_op)
### `get_beliefs_with_name_op`

#### Possible use: 
  * `agent` **`get_beliefs_with_name_op`** `string` --->  `msi.gama.util.IList<msi.gaml.architecture.simplebdi.MentalState>`
  *  **`get_beliefs_with_name_op`** (`agent` , `string`) --->  `msi.gama.util.IList<msi.gaml.architecture.simplebdi.MentalState>` 

#### Result: 
get the list of beliefs in the belief base which predicate has the given name.

#### Examples: 
```
get_beliefs_with_name_op(self,"has_water") 

```
  
    	
----

[//]: # (keyword|operator_get_current_intention_op)
### `get_current_intention_op`

#### Possible use: 
  *  **`get_current_intention_op`** (`agent`) --->  `mental_state` 

#### Result: 
get the current intention.

#### Examples: 
```
get_current_intention_op(self,has_water) 

```
  
    	
----

[//]: # (keyword|operator_get_decay)
### `get_decay`

#### Possible use: 
  *  **`get_decay`** (`emotion`) --->  `float` 

#### Result: 
get the decay value of the given emotion

#### Examples: 
```
get_decay(emotion) 

```
  
    	
----

[//]: # (keyword|operator_get_desire_op)
### `get_desire_op`

#### Possible use: 
  * `agent` **`get_desire_op`** `predicate` --->  `mental_state`
  *  **`get_desire_op`** (`agent` , `predicate`) --->  `mental_state` 

#### Result: 
get the desire in the desire base with the given predicate.

#### Examples: 
```
get_belief_op(self,has_water) 

```
  
    	
----

[//]: # (keyword|operator_get_desire_with_name_op)
### `get_desire_with_name_op`

#### Possible use: 
  * `agent` **`get_desire_with_name_op`** `string` --->  `mental_state`
  *  **`get_desire_with_name_op`** (`agent` , `string`) --->  `mental_state` 

#### Result: 
get the desire in the desire base with the given name.

#### Examples: 
```
 
mental_state var0 <- get_desire_with_name_op(self,"has_water"); // var0 equals nil

```
  
    	
----

[//]: # (keyword|operator_get_desires_op)
### `get_desires_op`

#### Possible use: 
  * `agent` **`get_desires_op`** `predicate` --->  `msi.gama.util.IList<msi.gaml.architecture.simplebdi.MentalState>`
  *  **`get_desires_op`** (`agent` , `predicate`) --->  `msi.gama.util.IList<msi.gaml.architecture.simplebdi.MentalState>` 

#### Result: 
get the desires in the desire base with the given predicate.

#### Examples: 
```
get_desires_op(self,has_water) 

```
  
    	
----

[//]: # (keyword|operator_get_desires_with_name_op)
### `get_desires_with_name_op`

#### Possible use: 
  * `agent` **`get_desires_with_name_op`** `string` --->  `msi.gama.util.IList<msi.gaml.architecture.simplebdi.MentalState>`
  *  **`get_desires_with_name_op`** (`agent` , `string`) --->  `msi.gama.util.IList<msi.gaml.architecture.simplebdi.MentalState>` 

#### Result: 
get the list of desires in the desire base which predicate has the given name.

#### Examples: 
```
get_desires_with_name_op(self,"has_water") 

```
  
    	
----

[//]: # (keyword|operator_get_dominance)
### `get_dominance`

#### Possible use: 
  *  **`get_dominance`** (`msi.gaml.architecture.simplebdi.SocialLink`) --->  `float` 

#### Result: 
get the dominance value of the given social link

#### Examples: 
```
get_dominance(social_link1) 

```
  
    	
----

[//]: # (keyword|operator_get_familiarity)
### `get_familiarity`

#### Possible use: 
  *  **`get_familiarity`** (`msi.gaml.architecture.simplebdi.SocialLink`) --->  `float` 

#### Result: 
get the familiarity value of the given social link

#### Examples: 
```
get_familiarity(social_link1) 

```
  
    	
----

[//]: # (keyword|operator_get_ideal_op)
### `get_ideal_op`

#### Possible use: 
  * `agent` **`get_ideal_op`** `predicate` --->  `mental_state`
  *  **`get_ideal_op`** (`agent` , `predicate`) --->  `mental_state` 

#### Result: 
get the ideal in the ideal base with the given name.

#### Examples: 
```
get_ideal_op(self,has_water) 

```
  
    	
----

[//]: # (keyword|operator_get_ideal_with_name_op)
### `get_ideal_with_name_op`

#### Possible use: 
  * `agent` **`get_ideal_with_name_op`** `string` --->  `mental_state`
  *  **`get_ideal_with_name_op`** (`agent` , `string`) --->  `mental_state` 

#### Result: 
get the ideal in the ideal base with the given name.

#### Examples: 
```
get_ideal_with_name_op(self,"has_water") 

```
  
    	
----

[//]: # (keyword|operator_get_ideals_op)
### `get_ideals_op`

#### Possible use: 
  * `agent` **`get_ideals_op`** `predicate` --->  `msi.gama.util.IList<msi.gaml.architecture.simplebdi.MentalState>`
  *  **`get_ideals_op`** (`agent` , `predicate`) --->  `msi.gama.util.IList<msi.gaml.architecture.simplebdi.MentalState>` 

#### Result: 
get the ideal in the ideal base with the given name.

#### Examples: 
```
get_ideals_op(self,has_water) 

```
  
    	
----

[//]: # (keyword|operator_get_ideals_with_name_op)
### `get_ideals_with_name_op`

#### Possible use: 
  * `agent` **`get_ideals_with_name_op`** `string` --->  `msi.gama.util.IList<msi.gaml.architecture.simplebdi.MentalState>`
  *  **`get_ideals_with_name_op`** (`agent` , `string`) --->  `msi.gama.util.IList<msi.gaml.architecture.simplebdi.MentalState>` 

#### Result: 
get the list of ideals in the ideal base which predicate has the given name.

#### Examples: 
```
get_ideals_with_name_op(self,"has_water") 

```
  
    	
----

[//]: # (keyword|operator_get_intensity)
### `get_intensity`

#### Possible use: 
  *  **`get_intensity`** (`emotion`) --->  `float` 

#### Result: 
get the intensity value of the given emotion

#### Examples: 
```
emotion set_intensity 12 

```
  
    	
----

[//]: # (keyword|operator_get_intention_op)
### `get_intention_op`

#### Possible use: 
  * `agent` **`get_intention_op`** `predicate` --->  `mental_state`
  *  **`get_intention_op`** (`agent` , `predicate`) --->  `mental_state` 

#### Result: 
get the intention in the intention base with the given predicate.

#### Examples: 
```
get_intention_op(self,has_water) 

```
  
    	
----

[//]: # (keyword|operator_get_intention_with_name_op)
### `get_intention_with_name_op`

#### Possible use: 
  * `agent` **`get_intention_with_name_op`** `string` --->  `mental_state`
  *  **`get_intention_with_name_op`** (`agent` , `string`) --->  `mental_state` 

#### Result: 
get the intention in the intention base with the given name.

#### Examples: 
```
get_intention_with_name_op(self,"has_water") 

```
  
    	
----

[//]: # (keyword|operator_get_intentions_op)
### `get_intentions_op`

#### Possible use: 
  * `agent` **`get_intentions_op`** `predicate` --->  `msi.gama.util.IList<msi.gaml.architecture.simplebdi.MentalState>`
  *  **`get_intentions_op`** (`agent` , `predicate`) --->  `msi.gama.util.IList<msi.gaml.architecture.simplebdi.MentalState>` 

#### Result: 
get the intentions in the intention base with the given predicate.

#### Examples: 
```
get_intentions_op(self,has_water) 

```
  
    	
----

[//]: # (keyword|operator_get_intentions_with_name_op)
### `get_intentions_with_name_op`

#### Possible use: 
  * `agent` **`get_intentions_with_name_op`** `string` --->  `msi.gama.util.IList<msi.gaml.architecture.simplebdi.MentalState>`
  *  **`get_intentions_with_name_op`** (`agent` , `string`) --->  `msi.gama.util.IList<msi.gaml.architecture.simplebdi.MentalState>` 

#### Result: 
get the list of intentions in the intention base which predicate has the given name.

#### Examples: 
```
get_intentions_with_name_op(self,"has_water") 

```
  
    	
----

[//]: # (keyword|operator_get_lifetime)
### `get_lifetime`

#### Possible use: 
  *  **`get_lifetime`** (`predicate`) --->  `int`
  *  **`get_lifetime`** (`mental_state`) --->  `int` 

#### Result: 
get the lifetime value of the given mental state

#### Examples: 
```
get_lifetime(mental_state1) 

```
  
    	
----

[//]: # (keyword|operator_get_liking)
### `get_liking`

#### Possible use: 
  *  **`get_liking`** (`msi.gaml.architecture.simplebdi.SocialLink`) --->  `float` 

#### Result: 
get the liking value of the given social link

#### Examples: 
```
get_liking(social_link1) 

```
  
    	
----

[//]: # (keyword|operator_get_modality)
### `get_modality`

#### Possible use: 
  *  **`get_modality`** (`mental_state`) --->  `string` 

#### Result: 
get the modality value of the given mental state

#### Examples: 
```
get_modality(mental_state1) 

```
  
    	
----

[//]: # (keyword|operator_get_obligation_op)
### `get_obligation_op`

#### Possible use: 
  * `agent` **`get_obligation_op`** `predicate` --->  `mental_state`
  *  **`get_obligation_op`** (`agent` , `predicate`) --->  `mental_state` 

#### Result: 
get the obligation in the obligation base with the given predicate.

#### Examples: 
```
get_obligation_op(self,has_water) 

```
  
    	
----

[//]: # (keyword|operator_get_obligation_with_name_op)
### `get_obligation_with_name_op`

#### Possible use: 
  * `agent` **`get_obligation_with_name_op`** `string` --->  `mental_state`
  *  **`get_obligation_with_name_op`** (`agent` , `string`) --->  `mental_state` 

#### Result: 
get the obligation in the obligation base with the given name.

#### Examples: 
```
get_obligation_with_name_op(self,"has_water") 

```
  
    	
----

[//]: # (keyword|operator_get_obligations_op)
### `get_obligations_op`

#### Possible use: 
  * `agent` **`get_obligations_op`** `predicate` --->  `msi.gama.util.IList<msi.gaml.architecture.simplebdi.MentalState>`
  *  **`get_obligations_op`** (`agent` , `predicate`) --->  `msi.gama.util.IList<msi.gaml.architecture.simplebdi.MentalState>` 

#### Result: 
get the obligations in the obligation base with the given predicate.

#### Examples: 
```
get_obligations_op(self,has_water) 

```
  
    	
----

[//]: # (keyword|operator_get_obligations_with_name_op)
### `get_obligations_with_name_op`

#### Possible use: 
  * `agent` **`get_obligations_with_name_op`** `string` --->  `msi.gama.util.IList<msi.gaml.architecture.simplebdi.MentalState>`
  *  **`get_obligations_with_name_op`** (`agent` , `string`) --->  `msi.gama.util.IList<msi.gaml.architecture.simplebdi.MentalState>` 

#### Result: 
get the list of obligations in the obligation base which predicate has the given name.

#### Examples: 
```
get_obligations_with_name_op(self,"has_water") 

```
  
    	
----

[//]: # (keyword|operator_get_plan_name)
### `get_plan_name`

#### Possible use: 
  *  **`get_plan_name`** (`BDIPlan`) --->  `string` 

#### Result: 
get the name of a given plan

#### Examples: 
```
get_plan_name(agent.current_plan) 

```
  
    	
----

[//]: # (keyword|operator_get_predicate)
### `get_predicate`

#### Possible use: 
  *  **`get_predicate`** (`mental_state`) --->  `predicate` 

#### Result: 
get the predicate value of the given mental state

#### Examples: 
```
get_predicate(mental_state1) 

```
  
    	
----

[//]: # (keyword|operator_get_solidarity)
### `get_solidarity`

#### Possible use: 
  *  **`get_solidarity`** (`msi.gaml.architecture.simplebdi.SocialLink`) --->  `float` 

#### Result: 
get the solidarity value of the given social link

#### Examples: 
```
get_solidarity(social_link1) 

```
  
    	
----

[//]: # (keyword|operator_get_strength)
### `get_strength`

#### Possible use: 
  *  **`get_strength`** (`mental_state`) --->  `float` 

#### Result: 
get the strength value of the given mental state

#### Examples: 
```
get_strength(mental_state1) 

```
  
    	
----

[//]: # (keyword|operator_get_super_intention)
### `get_super_intention`

#### Possible use: 
  *  **`get_super_intention`** (`predicate`) --->  `mental_state`
    	
----

[//]: # (keyword|operator_get_trust)
### `get_trust`

#### Possible use: 
  *  **`get_trust`** (`msi.gaml.architecture.simplebdi.SocialLink`) --->  `float` 

#### Result: 
get the familiarity value of the given social link

#### Examples: 
```
get_familiarity(social_link1) 

```
  
    	
----

[//]: # (keyword|operator_get_truth)
### `get_truth`

#### Possible use: 
  *  **`get_truth`** (`predicate`) --->  `bool`
    	
----

[//]: # (keyword|operator_get_uncertainties_op)
### `get_uncertainties_op`

#### Possible use: 
  * `agent` **`get_uncertainties_op`** `predicate` --->  `msi.gama.util.IList<msi.gaml.architecture.simplebdi.MentalState>`
  *  **`get_uncertainties_op`** (`agent` , `predicate`) --->  `msi.gama.util.IList<msi.gaml.architecture.simplebdi.MentalState>` 

#### Result: 
get the uncertainties in the uncertainty base with the given predicate.

#### Examples: 
```
get_uncertinties_op(self,has_water) 

```
  
    	
----

[//]: # (keyword|operator_get_uncertainties_with_name_op)
### `get_uncertainties_with_name_op`

#### Possible use: 
  * `agent` **`get_uncertainties_with_name_op`** `string` --->  `msi.gama.util.IList<msi.gaml.architecture.simplebdi.MentalState>`
  *  **`get_uncertainties_with_name_op`** (`agent` , `string`) --->  `msi.gama.util.IList<msi.gaml.architecture.simplebdi.MentalState>` 

#### Result: 
get the list of uncertainties in the uncertainty base which predicate has the given name.

#### Examples: 
```
get_uncertainties_with_name_op(self,"has_water") 

```
  
    	
----

[//]: # (keyword|operator_get_uncertainty_op)
### `get_uncertainty_op`

#### Possible use: 
  * `agent` **`get_uncertainty_op`** `predicate` --->  `mental_state`
  *  **`get_uncertainty_op`** (`agent` , `predicate`) --->  `mental_state` 

#### Result: 
get the uncertainty in the uncertainty base with the given predicate.

#### Examples: 
```
get_uncertainty_op(self,has_water) 

```
  
    	
----

[//]: # (keyword|operator_get_uncertainty_with_name_op)
### `get_uncertainty_with_name_op`

#### Possible use: 
  * `agent` **`get_uncertainty_with_name_op`** `string` --->  `mental_state`
  *  **`get_uncertainty_with_name_op`** (`agent` , `string`) --->  `mental_state` 

#### Result: 
get the uncertainty in the uncertainty base with the given name.

#### Examples: 
```
get_uncertainty_with_name_op(self,"has_water") 

```
  
    	
----

[//]: # (keyword|operator_gif_file)
### `gif_file`

#### Possible use: 
  *  **`gif_file`** (`string`) --->  `file` 

#### Result: 
Constructs a file of type gif. Allowed extensions are limited to gif
    	
----

[//]: # (keyword|operator_gini)
### `gini`

#### Possible use: 
  *  **`gini`** (`list<float>`) --->  `float`

#### Special cases:     
  * return the Gini Index of the given list of values (list of floats) 
  
```
 
float var0 <- gini([1.0, 0.5, 2.0]); // var0 equals the gini index computed
``` 


    	
----

[//]: # (keyword|operator_gml_file)
### `gml_file`

#### Possible use: 
  *  **`gml_file`** (`string`) --->  `file` 

#### Result: 
Constructs a file of type gml. Allowed extensions are limited to gml
    	
----

[//]: # (keyword|operator_graph)
### `graph`

#### Possible use: 
  *  **`graph`** (`any`) --->  `graph` 

#### Result: 
Casts the operand into the type graph
    	
----

[//]: # (keyword|operator_grayscale)
### `grayscale`

#### Possible use: 
  *  **`grayscale`** (`rgb`) --->  `rgb` 

#### Result: 
Converts rgb color to grayscale value  

#### Comment: 
r=red, g=green, b=blue. Between 0 and 255 and gray = 0.299 `*` red + 0.587 `*` green + 0.114 `*` blue (Photoshop value)

#### Examples: 
```
 
rgb var0 <- grayscale (rgb(255,0,0)); // var0 equals to a dark grey

```
      


#### See also: 

[rgb](operators-n-to-r#rgb), [hsb](operators-d-to-h#hsb), 
    	
----

[//]: # (keyword|operator_grid_at)
### `grid_at`

#### Possible use: 
  * `species` **`grid_at`** `point` --->  `agent`
  *  **`grid_at`** (`species` , `point`) --->  `agent` 

#### Result: 
returns the cell of the grid (right-hand operand) at the position given by the right-hand operand  

#### Comment: 
If the left-hand operand is a point of floats, it is used as a point of ints.

#### Special cases:     
  * if the left-hand operand is not a grid cell species, returns nil

#### Examples: 
```
 
agent var0 <- grid_cell grid_at {1,2}; // var0 equals the agent grid_cell with grid_x=1 and grid_y = 2

```
  
    	
----

[//]: # (keyword|operator_grid_cells_to_graph)
### `grid_cells_to_graph`

#### Possible use: 
  *  **`grid_cells_to_graph`** (`container`) --->  `graph` 

#### Result: 
creates a graph from a list of cells (operand). An edge is created between neighbors.

#### Examples: 
```
my_cell_graph<-grid_cells_to_graph(cells_list) 

```
  
    	
----

[//]: # (keyword|operator_grid_file)
### `grid_file`

#### Possible use: 
  *  **`grid_file`** (`string`) --->  `file` 

#### Result: 
Constructs a file of type grid. Allowed extensions are limited to asc, tif
    	
----

[//]: # (keyword|operator_group_by)
### `group_by`

#### Possible use: 
  * `container` **`group_by`** `any expression` --->  `map`
  *  **`group_by`** (`container` , `any expression`) --->  `map` 

#### Result: 
Returns a map, where the keys take the possible values of the right-hand operand and the map values are the list of elements of the left-hand operand associated to the key value  

#### Comment: 
in the right-hand operand, the keyword each can be used to represent, in turn, each of the right-hand operand elements.

#### Special cases:     
  * if the left-hand operand is nil, group_by throws an error

#### Examples: 
```
 
map var0 <- [1,2,3,4,5,6,7,8] group_by (each > 3); // var0 equals [false::[1, 2, 3], true::[4, 5, 6, 7, 8]] 
map var1 <- g2 group_by (length(g2 out_edges_of each) ); // var1 equals [ 0::[node9, node7, node10, node8, node11], 1::[node6], 2::[node5], 3::[node4]] 
map var2 <- (list(node) group_by (round(node(each).location.x)); // var2 equals [32::[node5], 21::[node1], 4::[node0], 66::[node2], 96::[node3]] 
map<bool,list> var3 <- [1::2, 3::4, 5::6] group_by (each > 4); // var3 equals [false::[2, 4], true::[6]]

```
      


#### See also: 

[first_with](operators-d-to-h#first_with), [last_with](operators-i-to-m#last_with), [where](operators-s-to-z#where), 
    	
----

[//]: # (keyword|operator_harmonic_mean)
### `harmonic_mean`

#### Possible use: 
  *  **`harmonic_mean`** (`container`) --->  `float` 

#### Result: 
the harmonic mean of the elements of the operand. See <A href="http://en.wikipedia.org/wiki/Harmonic_mean">Harmonic_mean</A> for more details.  

#### Comment: 
The operator casts all the numerical element of the list into float. The elements that are not numerical are discarded.

#### Examples: 
```
 
float var0 <- harmonic_mean ([4.5, 3.5, 5.5, 7.0]); // var0 equals 4.804159445407279

```
      


#### See also: 

[mean](operators-i-to-m#mean), [median](operators-i-to-m#median), [geometric_mean](operators-d-to-h#geometric_mean), 
    	
----

[//]: # (keyword|operator_has_belief_op)
### `has_belief_op`

#### Possible use: 
  * `agent` **`has_belief_op`** `predicate` --->  `bool`
  *  **`has_belief_op`** (`agent` , `predicate`) --->  `bool` 

#### Result: 
indicates if there already is a belief about the given predicate.

#### Examples: 
```
has_belief_op(self,has_water) 

```
  
    	
----

[//]: # (keyword|operator_has_belief_with_name_op)
### `has_belief_with_name_op`

#### Possible use: 
  * `agent` **`has_belief_with_name_op`** `string` --->  `bool`
  *  **`has_belief_with_name_op`** (`agent` , `string`) --->  `bool` 

#### Result: 
indicates if there already is a belief about the given name.

#### Examples: 
```
has_belief_with_name_op(self,"has_water") 

```
  
    	
----

[//]: # (keyword|operator_has_desire_op)
### `has_desire_op`

#### Possible use: 
  * `agent` **`has_desire_op`** `predicate` --->  `bool`
  *  **`has_desire_op`** (`agent` , `predicate`) --->  `bool` 

#### Result: 
indicates if there already is a desire about the given predicate.

#### Examples: 
```
has_desire_op(self,has_water) 

```
  
    	
----

[//]: # (keyword|operator_has_desire_with_name_op)
### `has_desire_with_name_op`

#### Possible use: 
  * `agent` **`has_desire_with_name_op`** `string` --->  `bool`
  *  **`has_desire_with_name_op`** (`agent` , `string`) --->  `bool` 

#### Result: 
indicates if there already is a desire about the given name.

#### Examples: 
```
has_desire_with_name_op(self,"has_water") 

```
  
    	
----

[//]: # (keyword|operator_has_ideal_op)
### `has_ideal_op`

#### Possible use: 
  * `agent` **`has_ideal_op`** `predicate` --->  `bool`
  *  **`has_ideal_op`** (`agent` , `predicate`) --->  `bool` 

#### Result: 
indicates if there already is an ideal about the given predicate.

#### Examples: 
```
has_ideal_op(self,has_water) 

```
  
    	
----

[//]: # (keyword|operator_has_ideal_with_name_op)
### `has_ideal_with_name_op`

#### Possible use: 
  * `agent` **`has_ideal_with_name_op`** `string` --->  `bool`
  *  **`has_ideal_with_name_op`** (`agent` , `string`) --->  `bool` 

#### Result: 
indicates if there already is an ideal about the given name.

#### Examples: 
```
has_ideal_with_name_op(self,"has_water") 

```
  
    	
----

[//]: # (keyword|operator_has_intention_op)
### `has_intention_op`

#### Possible use: 
  * `agent` **`has_intention_op`** `predicate` --->  `bool`
  *  **`has_intention_op`** (`agent` , `predicate`) --->  `bool` 

#### Result: 
indicates if there already is an intention about the given predicate.

#### Examples: 
```
has_intention_op(self,has_water) 

```
  
    	
----

[//]: # (keyword|operator_has_intention_with_name_op)
### `has_intention_with_name_op`

#### Possible use: 
  * `agent` **`has_intention_with_name_op`** `string` --->  `bool`
  *  **`has_intention_with_name_op`** (`agent` , `string`) --->  `bool` 

#### Result: 
indicates if there already is an intention about the given name.

#### Examples: 
```
has_intention_with_name_op(self,"has_water") 

```
  
    	
----

[//]: # (keyword|operator_has_obligation_op)
### `has_obligation_op`

#### Possible use: 
  * `agent` **`has_obligation_op`** `predicate` --->  `bool`
  *  **`has_obligation_op`** (`agent` , `predicate`) --->  `bool` 

#### Result: 
indicates if there already is an obligation about the given predicate.

#### Examples: 
```
has_obligation_op(self,has_water) 

```
  
    	
----

[//]: # (keyword|operator_has_obligation_with_name_op)
### `has_obligation_with_name_op`

#### Possible use: 
  * `agent` **`has_obligation_with_name_op`** `string` --->  `bool`
  *  **`has_obligation_with_name_op`** (`agent` , `string`) --->  `bool` 

#### Result: 
indicates if there already is an obligation about the given name.

#### Examples: 
```
has_obligation_with_name_op(self,"has_water") 

```
  
    	
----

[//]: # (keyword|operator_has_uncertainty_op)
### `has_uncertainty_op`

#### Possible use: 
  * `agent` **`has_uncertainty_op`** `predicate` --->  `bool`
  *  **`has_uncertainty_op`** (`agent` , `predicate`) --->  `bool` 

#### Result: 
indicates if there already is an uncertainty about the given predicate.

#### Examples: 
```
has_uncertainty_op(self,has_water) 

```
  
    	
----

[//]: # (keyword|operator_has_uncertainty_with_name_op)
### `has_uncertainty_with_name_op`

#### Possible use: 
  * `agent` **`has_uncertainty_with_name_op`** `string` --->  `bool`
  *  **`has_uncertainty_with_name_op`** (`agent` , `string`) --->  `bool` 

#### Result: 
indicates if there already is an uncertainty about the given name.

#### Examples: 
```
has_uncertainty_with_name_op(self,"has_water") 

```
  
    	
----

[//]: # (keyword|operator_hexagon)
### `hexagon`

#### Possible use: 
  *  **`hexagon`** (`float`) --->  `geometry`
  *  **`hexagon`** (`point`) --->  `geometry`
  * `float` **`hexagon`** `float` --->  `geometry`
  *  **`hexagon`** (`float` , `float`) --->  `geometry` 

#### Result: 
A hexagon geometry which the given with and height  

#### Comment: 
the center of the hexagon is by default the location of the current agent in which has been called this operator.the center of the hexagon is by default the location of the current agent in which has been called this operator.the center of the hexagon is by default the location of the current agent in which has been called this operator.

#### Special cases:     
  * returns nil if the operand is nil.    
  * returns nil if the operand is nil.    
  * returns nil if the operand is nil.

#### Examples: 
```
 
geometry var0 <- hexagon(10); // var0 equals a geometry as a hexagon of width of 10 and height of 10. 
geometry var1 <- hexagon({10,5}); // var1 equals a geometry as a hexagon of width of 10 and height of 5. 
geometry var2 <- hexagon(10,5); // var2 equals a geometry as a hexagon of width of 10 and height of 5.

```
      


#### See also: 

[around](operators-a-to-a#around), [circle](operators-b-to-c#circle), [cone](operators-b-to-c#cone), [line](operators-i-to-m#line), [link](operators-i-to-m#link), [norm](operators-n-to-r#norm), [point](operators-n-to-r#point), [polygon](operators-n-to-r#polygon), [polyline](operators-n-to-r#polyline), [rectangle](operators-n-to-r#rectangle), [triangle](operators-s-to-z#triangle), 
    	
----

[//]: # (keyword|operator_hierarchical_clustering)
### `hierarchical_clustering`

#### Possible use: 
  * `container<agent>` **`hierarchical_clustering`** `float` --->  `list`
  *  **`hierarchical_clustering`** (`container<agent>` , `float`) --->  `list` 

#### Result: 
A tree (list of list) contained groups of agents clustered by distance considering a distance min between two groups.  

#### Comment: 
use of hierarchical clustering with Minimum for linkage criterion between two groups of agents.

#### Examples: 
```
 
list var0 <- [ag1, ag2, ag3, ag4, ag5] hierarchical_clustering 20.0; // var0 equals for example, can return [[[ag1],[ag3]], [ag2], [[[ag4],[ag5]],[ag6]]

```
      


#### See also: 

[simple_clustering_by_distance](operators-s-to-z#simple_clustering_by_distance), 
    	
----

[//]: # (keyword|operator_horizontal)
### `horizontal`

#### Possible use: 
  *  **`horizontal`** (`msi.gama.util.GamaMap<java.lang.Object,java.lang.Integer>`) --->  `msi.gama.util.tree.GamaNode<java.lang.String>`
    	
----

[//]: # (keyword|operator_hsb)
### `hsb`

#### Possible use: 
  *  **`hsb`** (`float`, `float`, `float`) --->  `rgb`
  *  **`hsb`** (`float`, `float`, `float`, `float`) --->  `rgb`
  *  **`hsb`** (`float`, `float`, `float`, `int`) --->  `rgb` 

#### Result: 
Converts hsb (h=hue, s=saturation, b=brightness) value to Gama color  

#### Comment: 
h,s and b components should be floating-point values between 0.0 and 1.0 and when used alpha should be an integer (between 0 and 255) or a float (between 0 and 1) . Examples: Red=(0.0,1.0,1.0), Yellow=(0.16,1.0,1.0), Green=(0.33,1.0,1.0), Cyan=(0.5,1.0,1.0), Blue=(0.66,1.0,1.0), Magenta=(0.83,1.0,1.0)

#### Examples: 
```
 
rgb var0 <- hsb (0.0,1.0,1.0); // var0 equals rgb("red") 
rgb var1 <- hsb (0.5,1.0,1.0,0.0); // var1 equals rgb("cyan",0)

```
      


#### See also: 

[rgb](operators-n-to-r#rgb), 
    	
----

[//]: # (keyword|operator_hypot)
### `hypot`

#### Possible use: 
  *  **`hypot`** (`float`, `float`, `float`, `float`) --->  `float` 

#### Result: 
Returns sqrt(x2 +y2) without intermediate overflow or underflow.

#### Special cases:     
  * If either argument is infinite, then the result is positive infinity. If either argument is NaN and neither argument is infinite, then the result is NaN.

#### Examples: 
```
 
float var0 <- hypot(0,1,0,1); // var0 equals sqrt(2)

```
  