# Operators (S to Z)
 	


    	
----

[//]: # (keyword|operator_sample)
### `sample`

#### Possible use: 
  *  **`sample`** (`any expression`) --->  `string`
  * `string` **`sample`** `any expression` --->  `string`
  *  **`sample`** (`string` , `any expression`) --->  `string`
  *  **`sample`** (`list`, `int`, `bool`) --->  `list`
  *  **`sample`** (`list`, `int`, `bool`, `list`) --->  `list` 

#### Result: 
takes a sample of the specified size from the elements of x using either with or without replacement with given weights
takes a sample of the specified size from the elements of x using either with or without replacement

#### Examples: 
```
 
list var0 <- sample([2,10,1],2,false,[0.1,0.7,0.2]); // var0 equals [10,2] 
list var1 <- sample([2,10,1],2,false); // var1 equals [1,2]

```
  
    	
----

[//]: # (keyword|operator_Sanction)
### `Sanction`

#### Possible use: 
  *  **`Sanction`** (`any`) --->  `Sanction` 

#### Result: 
Casts the operand into the type Sanction
    	
----

[//]: # (keyword|operator_saveAgent)
### `saveAgent`

#### Possible use: 
  * `agent` **`saveAgent`** `string` --->  `int`
  *  **`saveAgent`** (`agent` , `string`) --->  `int`
    	
----

[//]: # (keyword|operator_saved_simulation_file)
### `saved_simulation_file`

#### Possible use: 
  *  **`saved_simulation_file`** (`string`) --->  `file` 

#### Result: 
Constructs a file of type saved_simulation. Allowed extensions are limited to gsim, gasim
    	
----

[//]: # (keyword|operator_saveSimulation)
### `saveSimulation`

#### Possible use: 
  *  **`saveSimulation`** (`string`) --->  `int`
    	
----

[//]: # (keyword|operator_scaled_by)
### `scaled_by`
   Same signification as [*](operators-a-to-a#*)
    	
----

[//]: # (keyword|operator_scaled_to)
### `scaled_to`

#### Possible use: 
  * `geometry` **`scaled_to`** `point` --->  `geometry`
  *  **`scaled_to`** (`geometry` , `point`) --->  `geometry` 

#### Result: 
allows to restrict the size of a geometry so that it fits in the envelope {width, height, depth} defined by the second operand

#### Examples: 
```
 
geometry var0 <- shape scaled_to {10,10}; // var0 equals a geometry corresponding to the geometry of the agent applying the operator scaled so that it fits a square of 10x10

```
  
    	
----

[//]: # (keyword|operator_select)
### `select`
   Same signification as [where](operators-s-to-z#where)
    	
----

[//]: # (keyword|operator_serialize)
### `serialize`

#### Possible use: 
  *  **`serialize`** (`unknown`) --->  `string` 

#### Result: 
It serializes any object, i.e. transform it into a string.
    	
----

[//]: # (keyword|operator_serializeAgent)
### `serializeAgent`

#### Possible use: 
  *  **`serializeAgent`** (`agent`) --->  `string`
    	
----

[//]: # (keyword|operator_set_about)
### `set_about`

#### Possible use: 
  * `emotion` **`set_about`** `predicate` --->  `emotion`
  *  **`set_about`** (`emotion` , `predicate`) --->  `emotion` 

#### Result: 
change the about value of the given emotion

#### Examples: 
```
emotion set_about predicate1 

```
  
    	
----

[//]: # (keyword|operator_set_agent)
### `set_agent`

#### Possible use: 
  * `msi.gaml.architecture.simplebdi.SocialLink` **`set_agent`** `agent` --->  `msi.gaml.architecture.simplebdi.SocialLink`
  *  **`set_agent`** (`msi.gaml.architecture.simplebdi.SocialLink` , `agent`) --->  `msi.gaml.architecture.simplebdi.SocialLink` 

#### Result: 
change the agent value of the given social link

#### Examples: 
```
social_link set_agent agentA 

```
  
    	
----

[//]: # (keyword|operator_set_agent_cause)
### `set_agent_cause`

#### Possible use: 
  * `predicate` **`set_agent_cause`** `agent` --->  `predicate`
  *  **`set_agent_cause`** (`predicate` , `agent`) --->  `predicate`
  * `emotion` **`set_agent_cause`** `agent` --->  `emotion`
  *  **`set_agent_cause`** (`emotion` , `agent`) --->  `emotion` 

#### Result: 
change the agentCause value of the given predicate
change the agentCause value of the given emotion

#### Examples: 
```
predicate set_agent_cause agentA emotion set_agent_cause agentA 

```
  
    	
----

[//]: # (keyword|operator_set_decay)
### `set_decay`

#### Possible use: 
  * `emotion` **`set_decay`** `float` --->  `emotion`
  *  **`set_decay`** (`emotion` , `float`) --->  `emotion` 

#### Result: 
change the decay value of the given emotion

#### Examples: 
```
emotion set_decay 12 

```
  
    	
----

[//]: # (keyword|operator_set_dominance)
### `set_dominance`

#### Possible use: 
  * `msi.gaml.architecture.simplebdi.SocialLink` **`set_dominance`** `float` --->  `msi.gaml.architecture.simplebdi.SocialLink`
  *  **`set_dominance`** (`msi.gaml.architecture.simplebdi.SocialLink` , `float`) --->  `msi.gaml.architecture.simplebdi.SocialLink` 

#### Result: 
change the dominance value of the given social link

#### Examples: 
```
social_link set_dominance 0.4 

```
  
    	
----

[//]: # (keyword|operator_set_familiarity)
### `set_familiarity`

#### Possible use: 
  * `msi.gaml.architecture.simplebdi.SocialLink` **`set_familiarity`** `float` --->  `msi.gaml.architecture.simplebdi.SocialLink`
  *  **`set_familiarity`** (`msi.gaml.architecture.simplebdi.SocialLink` , `float`) --->  `msi.gaml.architecture.simplebdi.SocialLink` 

#### Result: 
change the familiarity value of the given social link

#### Examples: 
```
social_link set_familiarity 0.4 

```
  
    	
----

[//]: # (keyword|operator_set_intensity)
### `set_intensity`

#### Possible use: 
  * `emotion` **`set_intensity`** `float` --->  `emotion`
  *  **`set_intensity`** (`emotion` , `float`) --->  `emotion` 

#### Result: 
change the intensity value of the given emotion

#### Examples: 
```
emotion set_intensity 12 

```
  
    	
----

[//]: # (keyword|operator_set_lifetime)
### `set_lifetime`

#### Possible use: 
  * `mental_state` **`set_lifetime`** `int` --->  `mental_state`
  *  **`set_lifetime`** (`mental_state` , `int`) --->  `mental_state` 

#### Result: 
change the lifetime value of the given mental state

#### Examples: 
```
mental state set_lifetime 1 

```
  
    	
----

[//]: # (keyword|operator_set_liking)
### `set_liking`

#### Possible use: 
  * `msi.gaml.architecture.simplebdi.SocialLink` **`set_liking`** `float` --->  `msi.gaml.architecture.simplebdi.SocialLink`
  *  **`set_liking`** (`msi.gaml.architecture.simplebdi.SocialLink` , `float`) --->  `msi.gaml.architecture.simplebdi.SocialLink` 

#### Result: 
change the liking value of the given social link

#### Examples: 
```
social_link set_liking 0.4 

```
  
    	
----

[//]: # (keyword|operator_set_modality)
### `set_modality`

#### Possible use: 
  * `mental_state` **`set_modality`** `string` --->  `mental_state`
  *  **`set_modality`** (`mental_state` , `string`) --->  `mental_state` 

#### Result: 
change the modality value of the given mental state

#### Examples: 
```
mental state set_modality belief 

```
  
    	
----

[//]: # (keyword|operator_set_predicate)
### `set_predicate`

#### Possible use: 
  * `mental_state` **`set_predicate`** `predicate` --->  `mental_state`
  *  **`set_predicate`** (`mental_state` , `predicate`) --->  `mental_state` 

#### Result: 
change the predicate value of the given mental state

#### Examples: 
```
mental state set_predicate pred1 

```
  
    	
----

[//]: # (keyword|operator_set_solidarity)
### `set_solidarity`

#### Possible use: 
  * `msi.gaml.architecture.simplebdi.SocialLink` **`set_solidarity`** `float` --->  `msi.gaml.architecture.simplebdi.SocialLink`
  *  **`set_solidarity`** (`msi.gaml.architecture.simplebdi.SocialLink` , `float`) --->  `msi.gaml.architecture.simplebdi.SocialLink` 

#### Result: 
change the solidarity value of the given social link

#### Examples: 
```
social_link set_solidarity 0.4 

```
  
    	
----

[//]: # (keyword|operator_set_strength)
### `set_strength`

#### Possible use: 
  * `mental_state` **`set_strength`** `float` --->  `mental_state`
  *  **`set_strength`** (`mental_state` , `float`) --->  `mental_state` 

#### Result: 
change the strength value of the given mental state

#### Examples: 
```
mental state set_strength 1.0 

```
  
    	
----

[//]: # (keyword|operator_set_trust)
### `set_trust`

#### Possible use: 
  * `msi.gaml.architecture.simplebdi.SocialLink` **`set_trust`** `float` --->  `msi.gaml.architecture.simplebdi.SocialLink`
  *  **`set_trust`** (`msi.gaml.architecture.simplebdi.SocialLink` , `float`) --->  `msi.gaml.architecture.simplebdi.SocialLink` 

#### Result: 
change the trust value of the given social link

#### Examples: 
```
social_link set_familiarity 0.4 

```
  
    	
----

[//]: # (keyword|operator_set_truth)
### `set_truth`

#### Possible use: 
  * `predicate` **`set_truth`** `bool` --->  `predicate`
  *  **`set_truth`** (`predicate` , `bool`) --->  `predicate` 

#### Result: 
change the is_true value of the given predicate

#### Examples: 
```
predicate set_truth false 

```
  
    	
----

[//]: # (keyword|operator_set_z)
### `set_z`

#### Possible use: 
  * `geometry` **`set_z`** `container<float>` --->  `geometry`
  *  **`set_z`** (`geometry` , `container<float>`) --->  `geometry`
  *  **`set_z`** (`geometry`, `int`, `float`) --->  `geometry` 

#### Result: 
Sets the z ordinate of the n-th point of a geometry to the value provided by the third argument

#### Examples: 
```
loop i from: 0 to: length(shape.points) - 1{set shape <-  set_z (shape, i, 3.0);} shape <- triangle(3) set_z [5,10,14]; 

```
  
    	
----

[//]: # (keyword|operator_shape_file)
### `shape_file`

#### Possible use: 
  *  **`shape_file`** (`string`) --->  `file` 

#### Result: 
Constructs a file of type shape. Allowed extensions are limited to shp
    	
----

[//]: # (keyword|operator_shuffle)
### `shuffle`

#### Possible use: 
  *  **`shuffle`** (`matrix`) --->  `matrix`
  *  **`shuffle`** (`string`) --->  `string`
  *  **`shuffle`** (`container`) --->  `list` 

#### Result: 
The elements of the operand in random order.

#### Special cases:     
  * if the operand is empty, returns an empty list (or string, matrix)

#### Examples: 
```
 
matrix var0 <- shuffle (matrix([["c11","c12","c13"],["c21","c22","c23"]])); // var0 equals matrix([["c12","c21","c11"],["c13","c22","c23"]]) (for example) 
string var1 <- shuffle ('abc'); // var1 equals 'bac' (for example) 
list var2 <- shuffle ([12, 13, 14]); // var2 equals [14,12,13] (for example)

```
      


#### See also: 

[reverse](operators-n-to-r#reverse), 
    	
----

[//]: # (keyword|operator_signum)
### `signum`

#### Possible use: 
  *  **`signum`** (`float`) --->  `int` 

#### Result: 
Returns -1 if the argument is negative, +1 if it is positive, 0 if it is equal to zero or not a number

#### Examples: 
```
 
int var0 <- signum(-12); // var0 equals -1 
int var1 <- signum(14); // var1 equals 1 
int var2 <- signum(0); // var2 equals 0

```
  
    	
----

[//]: # (keyword|operator_simple_clustering_by_distance)
### `simple_clustering_by_distance`

#### Possible use: 
  * `container<agent>` **`simple_clustering_by_distance`** `float` --->  `list<list<agent>>`
  *  **`simple_clustering_by_distance`** (`container<agent>` , `float`) --->  `list<list<agent>>` 

#### Result: 
A list of agent groups clustered by distance considering a distance min between two groups.

#### Examples: 
```
 
list<list<agent>> var0 <- [ag1, ag2, ag3, ag4, ag5] simpleClusteringByDistance 20.0; // var0 equals for example, can return [[ag1, ag3], [ag2], [ag4, ag5]]

```
      


#### See also: 

[hierarchical_clustering](operators-d-to-h#hierarchical_clustering), 
    	
----

[//]: # (keyword|operator_simple_clustering_by_envelope_distance)
### `simple_clustering_by_envelope_distance`
   Same signification as [simple_clustering_by_distance](operators-s-to-z#simple_clustering_by_distance)
    	
----

[//]: # (keyword|operator_simplex_generator)
### `simplex_generator`

#### Possible use: 
  *  **`simplex_generator`** (`float`, `float`, `float`) --->  `float` 

#### Result: 
take a x, y and a bias parameters and gives a value

#### Examples: 
```
 
float var0 <- simplex_generator(2,3,253); // var0 equals 10.2

```
  
    	
----

[//]: # (keyword|operator_simplification)
### `simplification`

#### Possible use: 
  * `geometry` **`simplification`** `float` --->  `geometry`
  *  **`simplification`** (`geometry` , `float`) --->  `geometry` 

#### Result: 
A geometry corresponding to the simplification of the operand (geometry, agent, point) considering a tolerance distance.  

#### Comment: 
The algorithm used for the simplification is Douglas-Peucker

#### Examples: 
```
 
geometry var0 <- self simplification 0.1; // var0 equals the geometry resulting from the application of the Douglas-Peuker algorithm on the geometry of the agent applying the operator with a tolerance distance of 0.1.

```
  
    	
----

[//]: # (keyword|operator_sin)
### `sin`

#### Possible use: 
  *  **`sin`** (`float`) --->  `float`
  *  **`sin`** (`int`) --->  `float` 

#### Result: 
Returns the value (in [-1,1]) of the sinus of the operand (in decimal degrees). The argument is casted to an int before being evaluated.

#### Special cases:     
  * Operand values out of the range [0-359] are normalized.

#### Examples: 
```
 
float var0 <- sin(360) with_precision 10 with_precision 10; // var0 equals 0.0 
float var1 <- sin (0); // var1 equals 0.0

```
      


#### See also: 

[cos](operators-b-to-c#cos), [tan](operators-s-to-z#tan), 
    	
----

[//]: # (keyword|operator_sin_rad)
### `sin_rad`

#### Possible use: 
  *  **`sin_rad`** (`float`) --->  `float` 

#### Result: 
Returns the value (in [-1,1]) of the sinus of the operand (in radians).

#### Examples: 
```
 
float var0 <- sin_rad(#pi); // var0 equals 0.0

```
      


#### See also: 

[cos_rad](operators-b-to-c#cos_rad), [tan_rad](operators-s-to-z#tan_rad), 
    	
----

[//]: # (keyword|operator_since)
### `since`

#### Possible use: 
  *  **`since`** (`date`) --->  `bool`
  * `any expression` **`since`** `date` --->  `bool`
  *  **`since`** (`any expression` , `date`) --->  `bool` 

#### Result: 
Returns true if the current_date of the model is after (or equal to) the date passed in argument. Synonym of 'current_date >= argument'. Can be used, like 'after', in its composed form with 2 arguments to express the lowest boundary of the computation of a frequency. However, contrary to 'after', there is a subtle difference: the lowest boundary will be tested against the frequency as well

#### Examples: 
```
reflex when: since(starting_date) {}  	// this reflex will always be run every(2#days) since (starting_date + 1#day) // the computation will return true 1 day after the starting date and every two days after this reference date 

```
  
    	
----

[//]: # (keyword|operator_skeletonize)
### `skeletonize`

#### Possible use: 
  *  **`skeletonize`** (`geometry`) --->  `list<geometry>`
  * `geometry` **`skeletonize`** `float` --->  `list<geometry>`
  *  **`skeletonize`** (`geometry` , `float`) --->  `list<geometry>`
  *  **`skeletonize`** (`geometry`, `float`, `float`) --->  `list<geometry>`
  *  **`skeletonize`** (`geometry`, `float`, `float`, `bool`) --->  `list<geometry>` 

#### Result: 
A list of geometries (polylines) corresponding to the skeleton of the operand geometry (geometry, agent) with the given tolerance for the clipping and for the triangulation
A list of geometries (polylines) corresponding to the skeleton of the operand geometry (geometry, agent)
A list of geometries (polylines) corresponding to the skeleton of the operand geometry (geometry, agent) with the given tolerance for the clipping and for the triangulation
A list of geometries (polylines) corresponding to the skeleton of the operand geometry (geometry, agent) with the given tolerance for the clipping

#### Examples: 
```
 
list<geometry> var0 <- skeletonize(self); // var0 equals the list of geometries corresponding to the skeleton of the geometry of the agent applying the operator. 
list<geometry> var1 <- skeletonize(self); // var1 equals the list of geometries corresponding to the skeleton of the geometry of the agent applying the operator. 
list<geometry> var2 <- skeletonize(self); // var2 equals the list of geometries corresponding to the skeleton of the geometry of the agent applying the operator. 
list<geometry> var3 <- skeletonize(self); // var3 equals the list of geometries corresponding to the skeleton of the geometry of the agent applying the operator.

```
  
    	
----

[//]: # (keyword|operator_skew)
### `skew`

#### Possible use: 
  *  **`skew`** (`container`) --->  `float`
  * `float` **`skew`** `float` --->  `float`
  *  **`skew`** (`float` , `float`) --->  `float` 

#### Result: 
Returns the skew of a data sequence, which is moment(data,3,mean) / standardDeviation3
Returns the skew of a data sequence.
    	
----

[//]: # (keyword|operator_skew_gauss)
### `skew_gauss`

#### Possible use: 
  *  **`skew_gauss`** (`float`, `float`, `float`, `float`) --->  `float` 

#### Result: 
A value from a skew normally distributed random variable with min value (the minimum skewed value possible), max value (the maximum skewed value possible), skew (the degree to which the values cluster around the mode of the distribution; higher values mean tighter clustering) and bias (the tendency of the mode to approach the min, max or midpoint value; positive values bias toward max, negative values toward min).The algorithm was taken from http://stackoverflow.com/questions/5853187/skewing-java-random-number-generation-toward-a-certain-number

#### Examples: 
```
 
float var0 <- skew_gauss(0.0, 1.0, 0.7,0.1); // var0 equals 0.1729218460343077

```
      


#### See also: 

[gauss](operators-d-to-h#gauss), [truncated_gauss](operators-s-to-z#truncated_gauss), [poisson](operators-n-to-r#poisson), 
    	
----

[//]: # (keyword|operator_skewness)
### `skewness`

#### Possible use: 
  *  **`skewness`** (`list`) --->  `float` 

#### Result: 
returns skewness value computed from the operand list of values

#### Special cases:     
  * if the length of the list is lower than 3, returns NaN

#### Examples: 
```
 
float var0 <- skewness ([1,2,3,4,5]); // var0 equals 0.0

```
  
    	
----

[//]: # (keyword|operator_skill)
### `skill`

#### Possible use: 
  *  **`skill`** (`any`) --->  `skill` 

#### Result: 
Casts the operand into the type skill
    	
----

[//]: # (keyword|operator_smooth)
### `smooth`

#### Possible use: 
  * `geometry` **`smooth`** `float` --->  `geometry`
  *  **`smooth`** (`geometry` , `float`) --->  `geometry` 

#### Result: 
Returns a 'smoothed' geometry, where straight lines are replaces by polynomial (bicubic) curves. The first parameter is the original geometry, the second is the 'fit' parameter which can be in the range 0 (loose fit) to 1 (tightest fit).

#### Examples: 
```
 
geometry var0 <- smooth(square(10), 0.0); // var0 equals a 'rounded' square

```
  
    	
----

[//]: # (keyword|operator_social_link)
### `social_link`

#### Possible use: 
  *  **`social_link`** (`any`) --->  `social_link` 

#### Result: 
Casts the operand into the type social_link
    	
----

[//]: # (keyword|operator_solid)
### `solid`
   Same signification as [without_holes](operators-s-to-z#without_holes)
    	
----

[//]: # (keyword|operator_sort)
### `sort`
   Same signification as [sort_by](operators-s-to-z#sort_by)
    	
----

[//]: # (keyword|operator_sort_by)
### `sort_by`

#### Possible use: 
  * `container` **`sort_by`** `any expression` --->  `list`
  *  **`sort_by`** (`container` , `any expression`) --->  `list` 

#### Result: 
Returns a list, containing the elements of the left-hand operand sorted in ascending order by the value of the right-hand operand when it is evaluated on them.  

#### Comment: 
the left-hand operand is casted to a list before applying the operator. In the right-hand operand, the keyword each can be used to represent, in turn, each of the elements.

#### Special cases:     
  * if the left-hand operand is nil, sort_by throws an error. If the sorting function returns values that cannot be compared, an error will be thrown as well

#### Examples: 
```
 
list var0 <- [1,2,4,3,5,7,6,8] sort_by (each); // var0 equals [1,2,3,4,5,6,7,8] 
list var2 <- g2 sort_by (length(g2 out_edges_of each) ); // var2 equals [node9, node7, node10, node8, node11, node6, node5, node4] 
list var3 <- (list(node) sort_by (round(node(each).location.x)); // var3 equals [node5, node1, node0, node2, node3] 
list var4 <- [1::2, 5::6, 3::4] sort_by (each); // var4 equals [2, 4, 6]

```
      


#### See also: 

[group_by](operators-d-to-h#group_by), 
    	
----

[//]: # (keyword|operator_source_of)
### `source_of`

#### Possible use: 
  * `graph` **`source_of`** `unknown` --->  `unknown`
  *  **`source_of`** (`graph` , `unknown`) --->  `unknown` 

#### Result: 
returns the source of the edge (right-hand operand) contained in the graph given in left-hand operand.

#### Special cases:     
  * if the lef-hand operand (the graph) is nil, throws an Exception

#### Examples: 
```
graph graphEpidemio <- generate_barabasi_albert( ["edges_species"::edge,"vertices_specy"::node,"size"::3,"m"::5] );  
unknown var1 <- graphEpidemio source_of(edge(3)); // var1 equals node1graph graphFromMap <-  as_edge_graph([{1,5}::{12,45},{12,45}::{34,56}]);  
point var3 <- graphFromMap source_of(link({1,5},{12,45})); // var3 equals {1,5}

```
      


#### See also: 

[target_of](operators-s-to-z#target_of), 
    	
----

[//]: # (keyword|operator_spatial_graph)
### `spatial_graph`

#### Possible use: 
  *  **`spatial_graph`** (`container`) --->  `graph` 

#### Result: 
allows to create a spatial graph from a container of vertices, without trying to wire them. The container can be empty. Emits an error if the contents of the container are not geometries, points or agents    


#### See also: 

[graph](operators-d-to-h#graph), 
    	
----

[//]: # (keyword|operator_species)
### `species`

#### Possible use: 
  *  **`species`** (`unknown`) --->  `species` 

#### Result: 
casting of the operand to a species.

#### Special cases:     
  * if the operand is nil, returns nil;    
  * if the operand is an agent, returns its species;    
  * if the operand is a string, returns the species with this name (nil if not found);    
  * otherwise, returns nil

#### Examples: 
```
 
species var0 <- species(self); // var0 equals the species of the current agent 
species var1 <- species('node'); // var1 equals node 
species var2 <- species([1,5,9,3]); // var2 equals nil 
species var3 <- species(node1); // var3 equals node

```
  
    	
----

[//]: # (keyword|operator_species_of)
### `species_of`
   Same signification as [species](operators-s-to-z#species)
    	
----

[//]: # (keyword|operator_sphere)
### `sphere`

#### Possible use: 
  *  **`sphere`** (`float`) --->  `geometry` 

#### Result: 
A sphere geometry which radius is equal to the operand.  

#### Comment: 
the centre of the sphere is by default the location of the current agent in which has been called this operator.

#### Special cases:     
  * returns a point if the operand is lower or equal to 0.

#### Examples: 
```
 
geometry var0 <- sphere(10); // var0 equals a geometry as a circle of radius 10 but displays a sphere.

```
      


#### See also: 

[around](operators-a-to-a#around), [cone](operators-b-to-c#cone), [line](operators-i-to-m#line), [link](operators-i-to-m#link), [norm](operators-n-to-r#norm), [point](operators-n-to-r#point), [polygon](operators-n-to-r#polygon), [polyline](operators-n-to-r#polyline), [rectangle](operators-n-to-r#rectangle), [square](operators-s-to-z#square), [triangle](operators-s-to-z#triangle), 
    	
----

[//]: # (keyword|operator_split)
### `split`

#### Possible use: 
  *  **`split`** (`list`) --->  `list<list>` 

#### Result: 
Splits a list of numbers into n=(1+3.3*log10(elements)) bins. The splitting is strict (i.e. elements are in the ith bin if they are strictly smaller than the ith bound    


#### See also: 

[split_in](operators-s-to-z#split_in), [split_using](operators-s-to-z#split_using), 
    	
----

[//]: # (keyword|operator_split_at)
### `split_at`

#### Possible use: 
  * `geometry` **`split_at`** `point` --->  `list<geometry>`
  *  **`split_at`** (`geometry` , `point`) --->  `list<geometry>` 

#### Result: 
The two part of the left-operand lines split at the given right-operand point

#### Special cases:     
  * if the left-operand is a point or a polygon, returns an empty list

#### Examples: 
```
 
list<geometry> var0 <- polyline([{1,2},{4,6}]) split_at {7,6}; // var0 equals [polyline([{1.0,2.0},{7.0,6.0}]), polyline([{7.0,6.0},{4.0,6.0}])]

```
  
    	
----

[//]: # (keyword|operator_split_geometry)
### `split_geometry`

#### Possible use: 
  * `geometry` **`split_geometry`** `point` --->  `list<geometry>`
  *  **`split_geometry`** (`geometry` , `point`) --->  `list<geometry>`
  * `geometry` **`split_geometry`** `float` --->  `list<geometry>`
  *  **`split_geometry`** (`geometry` , `float`) --->  `list<geometry>`
  *  **`split_geometry`** (`geometry`, `int`, `int`) --->  `list<geometry>` 

#### Result: 
A list of geometries that result from the decomposition of the geometry by rectangle cells of the given dimension (geometry, {size_x, size_y})
A list of geometries that result from the decomposition of the geometry according to a grid with the given number of rows and columns (geometry, nb_cols, nb_rows)
A list of geometries that result from the decomposition of the geometry by square cells of the given side size (geometry, size)

#### Examples: 
```
 
list<geometry> var0 <- to_rectangles(self, {10.0, 15.0}); // var0 equals the list of the geometries corresponding to the decomposition of the geometry by rectangles of size 10.0, 15.0 
list<geometry> var1 <- to_rectangles(self, 10,20); // var1 equals the list of the geometries corresponding to the decomposition of the geometry of the agent applying the operator 
list<geometry> var2 <- to_squares(self, 10.0); // var2 equals the list of the geometries corresponding to the decomposition of the geometry by squares of side size 10.0

```
  
    	
----

[//]: # (keyword|operator_split_in)
### `split_in`

#### Possible use: 
  * `list` **`split_in`** `int` --->  `list<list>`
  *  **`split_in`** (`list` , `int`) --->  `list<list>`
  *  **`split_in`** (`list`, `int`, `bool`) --->  `list<list>` 

#### Result: 
Splits a list of numbers into n bins defined by n-1 bounds between the minimum and maximum values found in the first argument. The boolean argument controls whether or not the splitting is strict (if true, elements are in the ith bin if they are strictly smaller than the ith bound
Splits a list of numbers into n bins defined by n-1 bounds between the minimum and maximum values found in the first argument. The splitting is strict (i.e. elements are in the ith bin if they are strictly smaller than the ith bound    


#### See also: 

[split](operators-s-to-z#split), [split_using](operators-s-to-z#split_using), 
    	
----

[//]: # (keyword|operator_split_lines)
### `split_lines`

#### Possible use: 
  *  **`split_lines`** (`container<geometry>`) --->  `list<geometry>`
  * `container<geometry>` **`split_lines`** `bool` --->  `list<geometry>`
  *  **`split_lines`** (`container<geometry>` , `bool`) --->  `list<geometry>` 

#### Result: 
A list of geometries resulting after cutting the lines at their intersections. if the last boolean operand is set to true, the split lines will import the attributes of the initial lines
A list of geometries resulting after cutting the lines at their intersections.

#### Examples: 
```
 
list<geometry> var0 <- split_lines([line([{0,10}, {20,10}]), line([{0,10}, {20,10}])]); // var0 equals a list of four polylines: line([{0,10}, {10,10}]), line([{10,10}, {20,10}]), line([{10,0}, {10,10}]) and line([{10,10}, {10,20}]) 
list<geometry> var1 <- split_lines([line([{0,10}, {20,10}]), line([{0,10}, {20,10}])]); // var1 equals a list of four polylines: line([{0,10}, {10,10}]), line([{10,10}, {20,10}]), line([{10,0}, {10,10}]) and line([{10,10}, {10,20}])

```
  
    	
----

[//]: # (keyword|operator_split_using)
### `split_using`

#### Possible use: 
  * `list` **`split_using`** `msi.gama.util.IList<? extends java.lang.Comparable>` --->  `list<list>`
  *  **`split_using`** (`list` , `msi.gama.util.IList<? extends java.lang.Comparable>`) --->  `list<list>`
  *  **`split_using`** (`list`, `msi.gama.util.IList<? extends java.lang.Comparable>`, `bool`) --->  `list<list>` 

#### Result: 
Splits a list of numbers into n+1 bins using a set of n bounds passed as the second argument. The boolean argument controls whether or not the splitting is strict (if true, elements are in the ith bin if they are strictly smaller than the ith bound
Splits a list of numbers into n+1 bins using a set of n bounds passed as the second argument. The splitting is strict (i.e. elements are in the ith bin if they are strictly smaller than the ith bound    


#### See also: 

[split](operators-s-to-z#split), [split_in](operators-s-to-z#split_in), 
    	
----

[//]: # (keyword|operator_split_with)
### `split_with`

#### Possible use: 
  * `string` **`split_with`** `string` --->  `list`
  *  **`split_with`** (`string` , `string`) --->  `list`
  *  **`split_with`** (`string`, `string`, `bool`) --->  `list` 

#### Result: 
Returns a list containing the sub-strings (tokens) of the left-hand operand delimited by each of the characters of the right-hand operand.
Returns a list containing the sub-strings (tokens) of the left-hand operand delimited either by each of the characters of the right-hand operand (false) or by the whole right-hand operand (true).  

#### Comment: 
Delimiters themselves are excluded from the resulting list.Delimiters themselves are excluded from the resulting list.

#### Examples: 
```
 
list var0 <- 'to be or not to be,that is the question' split_with ' ,'; // var0 equals ['to','be','or','not','to','be','that','is','the','question'] 
list var1 <- 'aa::bb:cc' split_with ('::', true); // var1 equals ['aa','bb:cc']

```
  
    	
----

[//]: # (keyword|operator_sqrt)
### `sqrt`

#### Possible use: 
  *  **`sqrt`** (`int`) --->  `float`
  *  **`sqrt`** (`float`) --->  `float` 

#### Result: 
Returns the square root of the operand.

#### Special cases:     
  * if the operand is negative, an exception is raised

#### Examples: 
```
 
float var0 <- sqrt(4); // var0 equals 2.0 
float var1 <- sqrt(4); // var1 equals 2.0

```
  
    	
----

[//]: # (keyword|operator_square)
### `square`

#### Possible use: 
  *  **`square`** (`float`) --->  `geometry` 

#### Result: 
A square geometry which side size is equal to the operand.  

#### Comment: 
the centre of the square is by default the location of the current agent in which has been called this operator.

#### Special cases:     
  * returns nil if the operand is nil.

#### Examples: 
```
 
geometry var0 <- square(10); // var0 equals a geometry as a square of side size 10.

```
      


#### See also: 

[around](operators-a-to-a#around), [circle](operators-b-to-c#circle), [cone](operators-b-to-c#cone), [line](operators-i-to-m#line), [link](operators-i-to-m#link), [norm](operators-n-to-r#norm), [point](operators-n-to-r#point), [polygon](operators-n-to-r#polygon), [polyline](operators-n-to-r#polyline), [rectangle](operators-n-to-r#rectangle), [triangle](operators-s-to-z#triangle), 
    	
----

[//]: # (keyword|operator_squircle)
### `squircle`

#### Possible use: 
  * `float` **`squircle`** `float` --->  `geometry`
  *  **`squircle`** (`float` , `float`) --->  `geometry` 

#### Result: 
A mix of square and circle geometry (see : http://en.wikipedia.org/wiki/Squircle), which side size is equal to the first operand and power is equal to the second operand  

#### Comment: 
the center of the ellipse is by default the location of the current agent in which has been called this operator.

#### Special cases:     
  * returns a point if the side operand is lower or equal to 0.

#### Examples: 
```
 
geometry var0 <- squircle(4,4); // var0 equals a geometry as a squircle of side 4 with a power of 4.

```
      


#### See also: 

[around](operators-a-to-a#around), [cone](operators-b-to-c#cone), [line](operators-i-to-m#line), [link](operators-i-to-m#link), [norm](operators-n-to-r#norm), [point](operators-n-to-r#point), [polygon](operators-n-to-r#polygon), [polyline](operators-n-to-r#polyline), [super_ellipse](operators-s-to-z#super_ellipse), [rectangle](operators-n-to-r#rectangle), [square](operators-s-to-z#square), [circle](operators-b-to-c#circle), [ellipse](operators-d-to-h#ellipse), [triangle](operators-s-to-z#triangle), 
    	
----

[//]: # (keyword|operator_stack)
### `stack`

#### Possible use: 
  *  **`stack`** (`msi.gama.util.IList<java.lang.Integer>`) --->  `msi.gama.util.tree.GamaNode<java.lang.String>`
    	
----

[//]: # (keyword|operator_standard_deviation)
### `standard_deviation`

#### Possible use: 
  *  **`standard_deviation`** (`container`) --->  `float` 

#### Result: 
the standard deviation on the elements of the operand. See <A href="http://en.wikipedia.org/wiki/Standard_deviation">Standard_deviation</A> for more details.  

#### Comment: 
The operator casts all the numerical element of the list into float. The elements that are not numerical are discarded.

#### Examples: 
```
 
float var0 <- standard_deviation ([4.5, 3.5, 5.5, 7.0]); // var0 equals 1.2930100540985752

```
      


#### See also: 

[mean](operators-i-to-m#mean), [mean_deviation](operators-i-to-m#mean_deviation), 
    	
----

[//]: # (keyword|operator_step_sub_model)
### `step_sub_model`

#### Possible use: 
  *  **`step_sub_model`** (`msi.gama.kernel.experiment.IExperimentAgent`) --->  `int` 

#### Result: 
Load a submodel  

#### Comment: 
loaded submodel
    	
----

[//]: # (keyword|operator_strahler)
### `strahler`

#### Possible use: 
  *  **`strahler`** (`graph`) --->  `map` 

#### Result: 
retur for each edge, its strahler number
    	
----

[//]: # (keyword|operator_string)
### `string`

#### Possible use: 
  * `date` **`string`** `string` --->  `string`
  *  **`string`** (`date` , `string`) --->  `string`
  *  **`string`** (`date`, `string`, `string`) --->  `string` 

#### Result: 
converts a date to astring following a custom pattern and using a specific locale (e.g.: 'fr', 'en', etc.). The pattern can use "%Y %M %N %D %E %h %m %s %z" for outputting years, months, name of month, days, name of days, hours, minutes, seconds and the time-zone. A null or empty pattern will return the complete date as defined by the ISO date & time format. The pattern can also follow the pattern definition found here, which gives much more control over the format of the date: https://docs.oracle.com/javase/8/docs/api/java/time/format/DateTimeFormatter.html#patterns. Different patterns are available by default as constants: #iso_local, #iso_simple, #iso_offset, #iso_zoned and #custom, which can be changed in the preferences
converts a date to astring following a custom pattern. The pattern can use "%Y %M %N %D %E %h %m %s %z" for outputting years, months, name of month, days, name of days, hours, minutes, seconds and the time-zone. A null or empty pattern will return the complete date as defined by the ISO date & time format. The pattern can also follow the pattern definition found here, which gives much more control over the format of the date: https://docs.oracle.com/javase/8/docs/api/java/time/format/DateTimeFormatter.html#patterns. Different patterns are available by default as constants: #iso_local, #iso_simple, #iso_offset, #iso_zoned and #custom, which can be changed in the preferences

#### Examples: 
```
format(#now, 'yyyy-MM-dd') format(#now, 'yyyy-MM-dd') 

```
  
    	
----

[//]: # (keyword|operator_student_area)
### `student_area`

#### Possible use: 
  * `float` **`student_area`** `int` --->  `float`
  *  **`student_area`** (`float` , `int`) --->  `float` 

#### Result: 
Returns the area to the left of x in the Student T distribution with the given degrees of freedom.
    	
----

[//]: # (keyword|operator_student_t_inverse)
### `student_t_inverse`

#### Possible use: 
  * `float` **`student_t_inverse`** `int` --->  `float`
  *  **`student_t_inverse`** (`float` , `int`) --->  `float` 

#### Result: 
Returns the value, t, for which the area under the Student-t probability density function (integrated from minus infinity to t) is equal to x.
    	
----

[//]: # (keyword|operator_subtract_days)
### `subtract_days`
   Same signification as [minus_days](operators-i-to-m#minus_days)
    	
----

[//]: # (keyword|operator_subtract_hours)
### `subtract_hours`
   Same signification as [minus_hours](operators-i-to-m#minus_hours)
    	
----

[//]: # (keyword|operator_subtract_minutes)
### `subtract_minutes`
   Same signification as [minus_minutes](operators-i-to-m#minus_minutes)
    	
----

[//]: # (keyword|operator_subtract_months)
### `subtract_months`
   Same signification as [minus_months](operators-i-to-m#minus_months)
    	
----

[//]: # (keyword|operator_subtract_ms)
### `subtract_ms`
   Same signification as [minus_ms](operators-i-to-m#minus_ms)
    	
----

[//]: # (keyword|operator_subtract_seconds)
### `subtract_seconds`
   Same signification as [-](operators-a-to-a#-)
    	
----

[//]: # (keyword|operator_subtract_weeks)
### `subtract_weeks`
   Same signification as [minus_weeks](operators-i-to-m#minus_weeks)
    	
----

[//]: # (keyword|operator_subtract_years)
### `subtract_years`
   Same signification as [minus_years](operators-i-to-m#minus_years)
    	
----

[//]: # (keyword|operator_successors_of)
### `successors_of`

#### Possible use: 
  * `graph` **`successors_of`** `unknown` --->  `list`
  *  **`successors_of`** (`graph` , `unknown`) --->  `list` 

#### Result: 
returns the list of successors (i.e. targets of out edges) of the given vertex (right-hand operand) in the given graph (left-hand operand)

#### Examples: 
```
 
list var1 <- graphEpidemio successors_of ({1,5}); // var1 equals [{12,45}] 
list var2 <- graphEpidemio successors_of node({34,56}); // var2 equals []

```
      


#### See also: 

[predecessors_of](operators-n-to-r#predecessors_of), [neighbors_of](operators-n-to-r#neighbors_of), 
    	
----

[//]: # (keyword|operator_sum)
### `sum`

#### Possible use: 
  *  **`sum`** (`graph`) --->  `float`
  *  **`sum`** (`container`) --->  `unknown` 

#### Result: 
the sum of all the elements of the operand  

#### Comment: 
the behavior depends on the nature of the operand

#### Special cases:     
  * if it is a population or a list of other types: sum transforms all elements into float and sums them    
  * if it is a map, sum returns the sum of the value of all elements    
  * if it is a file, sum returns the sum of the content of the file (that is also a container)    
  * if it is a graph, sum returns the total weight of the graph    
  * if it is a matrix of int, float or object, sum returns the sum of all the numerical elements (i.e. all elements for integer and float matrices)    
  * if it is a matrix of other types: sum transforms all elements into float and sums them    
  * if it is a list of colors: sum will sum them and return the blended resulting color    
  * if it is a list of int or float: sum returns the sum of all the elements 
  
```
 
int var0 <- sum ([12,10,3]); // var0 equals 25
``` 

    
  * if it is a list of points: sum returns the sum of all points as a point (each coordinate is the sum of the corresponding coordinate of each element) 
  
```
 
unknown var1 <- sum([{1.0,3.0},{3.0,5.0},{9.0,1.0},{7.0,8.0}]); // var1 equals {20.0,17.0}
``` 

    


#### See also: 

[mul](operators-i-to-m#mul), 
    	
----

[//]: # (keyword|operator_sum_of)
### `sum_of`

#### Possible use: 
  * `container` **`sum_of`** `any expression` --->  `unknown`
  *  **`sum_of`** (`container` , `any expression`) --->  `unknown` 

#### Result: 
the sum of the right-hand expression evaluated on each of the elements of the left-hand operand  

#### Comment: 
in the right-hand operand, the keyword each can be used to represent, in turn, each of the right-hand operand elements.

#### Special cases:     
  * if the left-operand is a map, the keyword each will contain each value 
  
```
 
unknown var1 <- [1::2, 3::4, 5::6] sum_of (each + 3); // var1 equals 21
``` 



#### Examples: 
```
 
unknown var0 <- [1,2] sum_of (each * 100 ); // var0 equals 300

```
      


#### See also: 

[min_of](operators-i-to-m#min_of), [max_of](operators-i-to-m#max_of), [product_of](operators-n-to-r#product_of), [mean_of](operators-i-to-m#mean_of), 
    	
----

[//]: # (keyword|operator_svg_file)
### `svg_file`

#### Possible use: 
  *  **`svg_file`** (`string`) --->  `file` 

#### Result: 
Constructs a file of type svg. Allowed extensions are limited to svg
    	
----

[//]: # (keyword|operator_tan)
### `tan`

#### Possible use: 
  *  **`tan`** (`int`) --->  `float`
  *  **`tan`** (`float`) --->  `float` 

#### Result: 
Returns the value (in [-1,1]) of the trigonometric tangent of the operand (in decimal degrees).

#### Special cases:     
  * Operand values out of the range [0-359] are normalized. Notice that tan(360) does not return 0.0 but -2.4492935982947064E-16    
  * The tangent is only defined for any real number except 90 + k `*` 180 (k an positive or negative integer). Nevertheless notice that tan(90) returns 1.633123935319537E16 (whereas we could except infinity).

#### Examples: 
```
 
float var0 <- tan (0); // var0 equals 0.0 
float var1 <- tan(90); // var1 equals 1.633123935319537E16

```
      


#### See also: 

[cos](operators-b-to-c#cos), [sin](operators-s-to-z#sin), 
    	
----

[//]: # (keyword|operator_tan_rad)
### `tan_rad`

#### Possible use: 
  *  **`tan_rad`** (`float`) --->  `float` 

#### Result: 
Returns the value (in [-1,1]) of the trigonometric tangent of the operand (in radians).    


#### See also: 

[cos_rad](operators-b-to-c#cos_rad), [sin_rad](operators-s-to-z#sin_rad), 
    	
----

[//]: # (keyword|operator_tanh)
### `tanh`

#### Possible use: 
  *  **`tanh`** (`int`) --->  `float`
  *  **`tanh`** (`float`) --->  `float` 

#### Result: 
Returns the value (in the interval [-1,1]) of the hyperbolic tangent of the operand (which can be any real number, expressed in decimal degrees).

#### Examples: 
```
 
float var0 <- tanh(0); // var0 equals 0.0 
float var1 <- tanh(100); // var1 equals 1.0

```
  
    	
----

[//]: # (keyword|operator_target_of)
### `target_of`

#### Possible use: 
  * `graph` **`target_of`** `unknown` --->  `unknown`
  *  **`target_of`** (`graph` , `unknown`) --->  `unknown` 

#### Result: 
returns the target of the edge (right-hand operand) contained in the graph given in left-hand operand.

#### Special cases:     
  * if the lef-hand operand (the graph) is nil, returns nil

#### Examples: 
```
graph graphEpidemio <- generate_barabasi_albert( ["edges_species"::edge,"vertices_specy"::node,"size"::3,"m"::5] );  
unknown var1 <- graphEpidemio source_of(edge(3)); // var1 equals node1graph graphFromMap <-  as_edge_graph([{1,5}::{12,45},{12,45}::{34,56}]);  
unknown var3 <- graphFromMap target_of(link({1,5},{12,45})); // var3 equals {12,45}

```
      


#### See also: 

[source_of](operators-s-to-z#source_of), 
    	
----

[//]: # (keyword|operator_teapot)
### `teapot`

#### Possible use: 
  *  **`teapot`** (`float`) --->  `geometry` 

#### Result: 
A teapot geometry which radius is equal to the operand.  

#### Comment: 
the centre of the teapot is by default the location of the current agent in which has been called this operator.

#### Special cases:     
  * returns a point if the operand is lower or equal to 0.

#### Examples: 
```
 
geometry var0 <- teapot(10); // var0 equals a geometry as a circle of radius 10 but displays a teapot.

```
      


#### See also: 

[around](operators-a-to-a#around), [cone](operators-b-to-c#cone), [line](operators-i-to-m#line), [link](operators-i-to-m#link), [norm](operators-n-to-r#norm), [point](operators-n-to-r#point), [polygon](operators-n-to-r#polygon), [polyline](operators-n-to-r#polyline), [rectangle](operators-n-to-r#rectangle), [square](operators-s-to-z#square), [triangle](operators-s-to-z#triangle), 
    	
----

[//]: # (keyword|operator_text_file)
### `text_file`

#### Possible use: 
  *  **`text_file`** (`string`) --->  `file` 

#### Result: 
Constructs a file of type text. Allowed extensions are limited to txt, data, text
    	
----

[//]: # (keyword|operator_TGauss)
### `TGauss`
   Same signification as [truncated_gauss](operators-s-to-z#truncated_gauss)
    	
----

[//]: # (keyword|operator_threeds_file)
### `threeds_file`

#### Possible use: 
  *  **`threeds_file`** (`string`) --->  `file` 

#### Result: 
Constructs a file of type threeds. Allowed extensions are limited to 3ds, max
    	
----

[//]: # (keyword|operator_to)
### `to`

#### Possible use: 
  * `date` **`to`** `date` --->  `msi.gama.util.IList<msi.gama.util.GamaDate>`
  *  **`to`** (`date` , `date`) --->  `msi.gama.util.IList<msi.gama.util.GamaDate>` 

#### Result: 
builds an interval between two dates (the first inclusive and the second exclusive, which behaves like a read-only list of dates. The default step between two dates is the step of the model  

#### Comment: 
The default step can be overruled by using the every operator applied to this interval

#### Examples: 
```
date('2000-01-01') to date('2010-01-01') // builds an interval between these two dates (date('2000-01-01') to date('2010-01-01')) every (#month) // builds an interval between these two dates which contains all the monthly dates starting from the beginning of the interval 

```
      


#### See also: 

[every](operators-d-to-h#every), 
    	
----

[//]: # (keyword|operator_to_GAMA_CRS)
### `to_GAMA_CRS`

#### Possible use: 
  *  **`to_GAMA_CRS`** (`geometry`) --->  `geometry`
  * `geometry` **`to_GAMA_CRS`** `string` --->  `geometry`
  *  **`to_GAMA_CRS`** (`geometry` , `string`) --->  `geometry`

#### Special cases:     
  * returns the geometry corresponding to the transformation of the given geometry to the GAMA CRS (Coordinate Reference System) assuming the given geometry is referenced by given CRS 
  
```
 
geometry var0 <- to_GAMA_CRS({121,14}, "EPSG:4326"); // var0 equals a geometry corresponding to the agent geometry transformed into the GAMA CRS
``` 

    
  * returns the geometry corresponding to the transformation of the given geometry to the GAMA CRS (Coordinate Reference System) assuming the given geometry is referenced by the current CRS, the one corresponding to the world's agent one 
  
```
 
geometry var1 <- to_GAMA_CRS({121,14}); // var1 equals a geometry corresponding to the agent geometry transformed into the GAMA CRS
``` 


    	
----

[//]: # (keyword|operator_to_gaml)
### `to_gaml`

#### Possible use: 
  *  **`to_gaml`** (`unknown`) --->  `string` 

#### Result: 
returns the literal description of an expression or description -- action, behavior, species, aspect, even model -- in gaml

#### Examples: 
```
 
string var0 <- to_gaml(0); // var0 equals '0' 
string var1 <- to_gaml(3.78); // var1 equals '3.78' 
string var2 <- to_gaml(true); // var2 equals 'true' 
string var3 <- to_gaml({23, 4.0}); // var3 equals '{23.0,4.0,0.0}' 
string var4 <- to_gaml(5::34); // var4 equals '5::34' 
string var5 <- to_gaml(rgb(255,0,125)); // var5 equals 'rgb (255, 0, 125,255)' 
string var6 <- to_gaml('hello'); // var6 equals "'hello'" 
string var7 <- to_gaml([1,5,9,3]); // var7 equals '[1,5,9,3]' 
string var8 <- to_gaml(['a'::345, 'b'::13, 'c'::12]); // var8 equals "map(['a'::345,'b'::13,'c'::12])" 
string var9 <- to_gaml([[3,5,7,9],[2,4,6,8]]); // var9 equals '[[3,5,7,9],[2,4,6,8]]' 
string var10 <- to_gaml(a_graph); // var10 equals ([((1 as node)::(3 as node))::(5 as edge),((0 as node)::(3 as node))::(3 as edge),((1 as node)::(2 as node))::(1 as edge),((0 as node)::(2 as node))::(2 as edge),((0 as node)::(1 as node))::(0 as edge),((2 as node)::(3 as node))::(4 as edge)] as map ) as graph 
string var11 <- to_gaml(node1); // var11 equals  1 as node

```
  
    	
----

[//]: # (keyword|operator_to_rectangles)
### `to_rectangles`
   Same signification as [split_geometry](operators-s-to-z#split_geometry)

#### Possible use: 
  *  **`to_rectangles`** (`geometry`, `point`, `bool`) --->  `list<geometry>`
  *  **`to_rectangles`** (`geometry`, `int`, `int`, `bool`) --->  `list<geometry>` 

#### Result: 
A list of rectangles corresponding to the given dimension that result from the decomposition of the geometry into rectangles (geometry, nb_cols, nb_rows, overlaps) by a grid composed of the given number of columns and rows, if overlaps = true, add the rectangles that overlap the border of the geometry
A list of rectangles of the size corresponding to the given dimension that result from the decomposition of the geometry into rectangles (geometry, dimension, overlaps), if overlaps = true, add the rectangles that overlap the border of the geometry

#### Examples: 
```
 
list<geometry> var0 <- to_rectangles(self, 5, 20, true); // var0 equals the list of rectangles corresponding to the discretization by a grid of 5 columns and 20 rows into rectangles of the geometry of the agent applying the operator. The rectangles overlapping the border of the geometry are kept 
list<geometry> var1 <- to_rectangles(self, {10.0, 15.0}, true); // var1 equals the list of rectangles of size {10.0, 15.0} corresponding to the discretization into rectangles of the geometry of the agent applying the operator. The rectangles overlapping the border of the geometry are kept

```
  
    	
----

[//]: # (keyword|operator_to_squares)
### `to_squares`

#### Possible use: 
  *  **`to_squares`** (`geometry`, `int`, `bool`) --->  `list<geometry>`
  *  **`to_squares`** (`geometry`, `float`, `bool`) --->  `list<geometry>`
  *  **`to_squares`** (`geometry`, `int`, `bool`, `float`) --->  `list<geometry>` 

#### Result: 
A list of a given number of squares from the decomposition of the geometry into squares (geometry, nb_square, overlaps, precision_coefficient), if overlaps = true, add the squares that overlap the border of the geometry, coefficient_precision should be close to 1.0
A list of a given number of squares from the decomposition of the geometry into squares (geometry, nb_square, overlaps), if overlaps = true, add the squares that overlap the border of the geometry
A list of squares of the size corresponding to the given size that result from the decomposition of the geometry into squares (geometry, size, overlaps), if overlaps = true, add the squares that overlap the border of the geometry

#### Examples: 
```
 
list<geometry> var0 <- to_squares(self, 10, true, 0.99); // var0 equals the list of 10 squares corresponding to the discretization into squares of the geometry of the agent applying the operator. The squares overlapping the border of the geometry are kept 
list<geometry> var1 <- to_squares(self, 10, true); // var1 equals the list of 10 squares corresponding to the discretization into squares of the geometry of the agent applying the operator. The squares overlapping the border of the geometry are kept 
list<geometry> var2 <- to_squares(self, 10.0, true); // var2 equals the list of squares of side size 10.0 corresponding to the discretization into squares of the geometry of the agent applying the operator. The squares overlapping the border of the geometry are kept

```
  
    	
----

[//]: # (keyword|operator_to_sub_geometries)
### `to_sub_geometries`

#### Possible use: 
  * `geometry` **`to_sub_geometries`** `list<float>` --->  `list<geometry>`
  *  **`to_sub_geometries`** (`geometry` , `list<float>`) --->  `list<geometry>`
  *  **`to_sub_geometries`** (`geometry`, `list<float>`, `float`) --->  `list<geometry>` 

#### Result: 
A list of geometries resulting after spliting the geometry into sub-geometries.
A list of geometries resulting after spliting the geometry into sub-geometries.

#### Examples: 
```
 
list<geometry> var0 <- to_sub_geometries(rectangle(10, 50), [0.1, 0.5, 0.4], 1.0); // var0 equals a list of three geometries corresponding to 3 sub-geometries using cubes of 1m size 
list<geometry> var1 <- to_sub_geometries(rectangle(10, 50), [0.1, 0.5, 0.4]); // var1 equals a list of three geometries corresponding to 3 sub-geometries

```
  
    	
----

[//]: # (keyword|operator_to_triangles)
### `to_triangles`
   Same signification as [triangulate](operators-s-to-z#triangulate)
    	
----

[//]: # (keyword|operator_tokenize)
### `tokenize`
   Same signification as [split_with](operators-s-to-z#split_with)
    	
----

[//]: # (keyword|operator_topology)
### `topology`

#### Possible use: 
  *  **`topology`** (`unknown`) --->  `topology` 

#### Result: 
casting of the operand to a topology.

#### Special cases:     
  * if the operand is a topology, returns the topology itself;    
  * if the operand is a spatial graph, returns the graph topology associated;    
  * if the operand is a population, returns the topology of the population;    
  * if the operand is a shape or a geometry, returns the continuous topology bounded by the geometry;    
  * if the operand is a matrix, returns the grid topology associated    
  * if the operand is another kind of container, returns the multiple topology associated to the container    
  * otherwise, casts the operand to a geometry and build a topology from it.

#### Examples: 
```
 
topology var0 <- topology(0); // var0 equals niltopology(a_graph)	--: Multiple topology in POLYGON ((24.712119771887785 7.867357373616512, 24.712119771887785 61.283226839310565, 82.4013676510046  7.867357373616512)) at location[53.556743711446195;34.57529210646354] 

```
      


#### See also: 

[geometry](operators-d-to-h#geometry), 
    	
----

[//]: # (keyword|operator_topology)
### `topology`

#### Possible use: 
  *  **`topology`** (`any`) --->  `topology` 

#### Result: 
Casts the operand into the type topology
    	
----

[//]: # (keyword|operator_touches)
### `touches`

#### Possible use: 
  * `geometry` **`touches`** `geometry` --->  `bool`
  *  **`touches`** (`geometry` , `geometry`) --->  `bool` 

#### Result: 
A boolean, equal to true if the left-geometry (or agent/point) touches the right-geometry (or agent/point).  

#### Comment: 
returns true when the left-operand only touches the right-operand. When one geometry covers partially (or fully) the other one, it returns false.

#### Special cases:     
  * if one of the operand is null, returns false.

#### Examples: 
```
 
bool var0 <- polyline([{10,10},{20,20}]) touches {15,15}; // var0 equals false 
bool var1 <- polyline([{10,10},{20,20}]) touches {10,10}; // var1 equals true 
bool var2 <- {15,15} touches {15,15}; // var2 equals false 
bool var3 <- polyline([{10,10},{20,20}]) touches polyline([{10,10},{5,5}]); // var3 equals true 
bool var4 <- polyline([{10,10},{20,20}]) touches polyline([{5,5},{15,15}]); // var4 equals false 
bool var5 <- polyline([{10,10},{20,20}]) touches polyline([{15,15},{25,25}]); // var5 equals false 
bool var6 <- polygon([{10,10},{10,20},{20,20},{20,10}]) touches polygon([{15,15},{15,25},{25,25},{25,15}]); // var6 equals false 
bool var7 <- polygon([{10,10},{10,20},{20,20},{20,10}]) touches polygon([{10,20},{20,20},{20,30},{10,30}]); // var7 equals true 
bool var8 <- polygon([{10,10},{10,20},{20,20},{20,10}]) touches polygon([{10,10},{0,10},{0,0},{10,0}]); // var8 equals true 
bool var9 <- polygon([{10,10},{10,20},{20,20},{20,10}]) touches {15,15}; // var9 equals false 
bool var10 <- polygon([{10,10},{10,20},{20,20},{20,10}]) touches {10,15}; // var10 equals true

```
      


#### See also: 

[disjoint_from](operators-d-to-h#disjoint_from), [crosses](operators-b-to-c#crosses), [overlaps](operators-n-to-r#overlaps), [partially_overlaps](operators-n-to-r#partially_overlaps), [intersects](operators-i-to-m#intersects), 
    	
----

[//]: # (keyword|operator_towards)
### `towards`

#### Possible use: 
  * `geometry` **`towards`** `geometry` --->  `float`
  *  **`towards`** (`geometry` , `geometry`) --->  `float` 

#### Result: 
The direction (in degree) between the two geometries (geometries, agents, points) considering the topology of the agent applying the operator.

#### Examples: 
```
 
float var0 <- ag1 towards ag2; // var0 equals the direction between ag1 and ag2 and ag3 considering the topology of the agent applying the operator

```
      


#### See also: 

[distance_between](operators-d-to-h#distance_between), [distance_to](operators-d-to-h#distance_to), [direction_between](operators-d-to-h#direction_between), [path_between](operators-n-to-r#path_between), [path_to](operators-n-to-r#path_to), 
    	
----

[//]: # (keyword|operator_trace)
### `trace`

#### Possible use: 
  *  **`trace`** (`matrix`) --->  `float` 

#### Result: 
The trace of the given matrix (the sum of the elements on the main diagonal).

#### Examples: 
```
 
float var0 <- trace(matrix([[1,2],[3,4]])); // var0 equals 5

```
  
    	
----

[//]: # (keyword|operator_transformed_by)
### `transformed_by`

#### Possible use: 
  * `geometry` **`transformed_by`** `point` --->  `geometry`
  *  **`transformed_by`** (`geometry` , `point`) --->  `geometry` 

#### Result: 
A geometry resulting from the application of a rotation and a scaling (right-operand : point {angle(degree), scale factor} of the left-hand operand (geometry, agent, point)

#### Examples: 
```
 
geometry var0 <- self transformed_by {45, 0.5}; // var0 equals the geometry resulting from 45 degrees rotation and 50% scaling of the geometry of the agent applying the operator.

```
      


#### See also: 

[rotated_by](operators-n-to-r#rotated_by), [translated_by](operators-s-to-z#translated_by), 
    	
----

[//]: # (keyword|operator_translated_by)
### `translated_by`

#### Possible use: 
  * `geometry` **`translated_by`** `point` --->  `geometry`
  *  **`translated_by`** (`geometry` , `point`) --->  `geometry` 

#### Result: 
A geometry resulting from the application of a translation by the right-hand operand distance to the left-hand operand (geometry, agent, point)

#### Examples: 
```
 
geometry var0 <- self translated_by {10,10,10}; // var0 equals the geometry resulting from applying the translation to the left-hand geometry (or agent).

```
      


#### See also: 

[rotated_by](operators-n-to-r#rotated_by), [transformed_by](operators-s-to-z#transformed_by), 
    	
----

[//]: # (keyword|operator_translated_to)
### `translated_to`
   Same signification as [at_location](operators-a-to-a#at_location)
    	
----

[//]: # (keyword|operator_transpose)
### `transpose`

#### Possible use: 
  *  **`transpose`** (`matrix`) --->  `matrix` 

#### Result: 
The transposition of the given matrix

#### Examples: 
```
 
matrix var0 <- transpose(matrix([[5,-3],[6,-4]])); // var0 equals matrix([[5,6],[-3,-4]])

```
  
    	
----

[//]: # (keyword|operator_triangle)
### `triangle`

#### Possible use: 
  *  **`triangle`** (`float`) --->  `geometry` 

#### Result: 
A triangle geometry which side size is given by the operand.  

#### Comment: 
the center of the triangle is by default the location of the current agent in which has been called this operator.

#### Special cases:     
  * returns nil if the operand is nil.

#### Examples: 
```
 
geometry var0 <- triangle(5); // var0 equals a geometry as a triangle with side_size = 5.

```
      


#### See also: 

[around](operators-a-to-a#around), [circle](operators-b-to-c#circle), [cone](operators-b-to-c#cone), [line](operators-i-to-m#line), [link](operators-i-to-m#link), [norm](operators-n-to-r#norm), [point](operators-n-to-r#point), [polygon](operators-n-to-r#polygon), [polyline](operators-n-to-r#polyline), [rectangle](operators-n-to-r#rectangle), [square](operators-s-to-z#square), 
    	
----

[//]: # (keyword|operator_triangulate)
### `triangulate`

#### Possible use: 
  *  **`triangulate`** (`geometry`) --->  `list<geometry>`
  *  **`triangulate`** (`list<geometry>`) --->  `list<geometry>`
  * `geometry` **`triangulate`** `float` --->  `list<geometry>`
  *  **`triangulate`** (`geometry` , `float`) --->  `list<geometry>`
  *  **`triangulate`** (`geometry`, `float`, `float`) --->  `list<geometry>`
  *  **`triangulate`** (`geometry`, `float`, `float`, `bool`) --->  `list<geometry>` 

#### Result: 
A list of geometries (triangles) corresponding to the Delaunay triangulation of the operand geometry (geometry, agent, point)
A list of geometries (triangles) corresponding to the Delaunay triangulation of the operand geometry (geometry, agent, point) with the given tolerance for the clipping and for the triangulation
A list of geometries (triangles) corresponding to the Delaunay triangulation of the operand geometry (geometry, agent, point) with the given tolerance for the clipping
A list of geometries (triangles) corresponding to the Delaunay triangulation computed from the list of polylines
A list of geometries (triangles) corresponding to the Delaunay triangulation of the operand geometry (geometry, agent, point, use_approx_clipping) with the given tolerance for the clipping and for the triangulation with using an approximate clipping is the last operand is true

#### Examples: 
```
 
list<geometry> var0 <- triangulate(self); // var0 equals the list of geometries (triangles) corresponding to the Delaunay triangulation of the geometry of the agent applying the operator. 
list<geometry> var1 <- triangulate(self,0.1, 1.0); // var1 equals the list of geometries (triangles) corresponding to the Delaunay triangulation of the geometry of the agent applying the operator. 
list<geometry> var2 <- triangulate(self, 0.1); // var2 equals the list of geometries (triangles) corresponding to the Delaunay triangulation of the geometry of the agent applying the operator. 
list<geometry> var3 <- triangulate([line([{0,50},{100,50}]), line([{50,0},{50,100}])); // var3 equals the list of geometries (triangles) corresponding to the Delaunay triangulation of the geometry of the agent applying the operator. 
list<geometry> var4 <- triangulate(self,0.1, 1.0); // var4 equals the list of geometries (triangles) corresponding to the Delaunay triangulation of the geometry of the agent applying the operator.

```
  
    	
----

[//]: # (keyword|operator_truncated_gauss)
### `truncated_gauss`

#### Possible use: 
  *  **`truncated_gauss`** (`point`) --->  `float`
  *  **`truncated_gauss`** (`list`) --->  `float` 

#### Result: 
A random value from a normally distributed random variable in the interval ]mean - standardDeviation; mean + standardDeviation[.

#### Special cases:     
  * when the operand is a point, it is read as {mean, standardDeviation}    
  * if the operand is a list, only the two first elements are taken into account as [mean, standardDeviation]    
  * when truncated_gauss is called with a list of only one element mean, it will always return 0.0

#### Examples: 
```
 
float var0 <- truncated_gauss ({0, 0.3}); // var0 equals a float between -0.3 and 0.3 
float var1 <- truncated_gauss ([0.5, 0.0]); // var1 equals 0.5

```
      


#### See also: 

[gauss](operators-d-to-h#gauss), 
    	
----

[//]: # (keyword|operator_type_of)
### `type_of`

#### Possible use: 
  *  **`type_of`** (`unknown`) --->  `msi.gaml.types.IType<?>`
    	
----

[//]: # (keyword|operator_undirected)
### `undirected`

#### Possible use: 
  *  **`undirected`** (`graph`) --->  `graph` 

#### Result: 
the operand graph becomes an undirected graph.  

#### Comment: 
the operator alters the operand graph, it does not create a new one.    


#### See also: 

[directed](operators-d-to-h#directed), 
    	
----

[//]: # (keyword|operator_union)
### `union`

#### Possible use: 
  *  **`union`** (`container<geometry>`) --->  `geometry`
  * `container` **`union`** `container` --->  `list`
  *  **`union`** (`container` , `container`) --->  `list` 

#### Result: 
returns a new list containing all the elements of both containers without duplicated elements.

#### Special cases:     
  * if the left or right operand is nil, union throws an error    
  * if the right-operand is a container of points, geometries or agents, returns the geometry resulting from the union all the geometries

#### Examples: 
```
 
list var0 <- [1,2,3,4,5,6] union [2,4,9]; // var0 equals [1,2,3,4,5,6,9] 
list var1 <- [1,2,3,4,5,6] union [0,8]; // var1 equals [1,2,3,4,5,6,0,8] 
list var2 <- [1,3,2,4,5,6,8,5,6] union [0,8]; // var2 equals [1,3,2,4,5,6,8,0] 
geometry var3 <- union([geom1, geom2, geom3]); // var3 equals a geometry corresponding to union between geom1, geom2 and geom3

```
      


#### See also: 

[inter](operators-i-to-m#inter), [+](operators-a-to-a#+), 
    	
----

[//]: # (keyword|operator_unknown)
### `unknown`

#### Possible use: 
  *  **`unknown`** (`any`) --->  `unknown` 

#### Result: 
Casts the operand into the type unknown
    	
----

[//]: # (keyword|operator_until)
### `until`

#### Possible use: 
  *  **`until`** (`date`) --->  `bool`
  * `any expression` **`until`** `date` --->  `bool`
  *  **`until`** (`any expression` , `date`) --->  `bool` 

#### Result: 
Returns true if the current_date of the model is before (or equel to) the date passed in argument. Synonym of 'current_date <= argument'

#### Examples: 
```
reflex when: until(starting_date) {} 	// This reflex will be run only once at the beginning of the simulation 

```
  
    	
----

[//]: # (keyword|operator_upper_case)
### `upper_case`

#### Possible use: 
  *  **`upper_case`** (`string`) --->  `string` 

#### Result: 
Converts all of the characters in the string operand to upper case

#### Examples: 
```
 
string var0 <- upper_case("Abc"); // var0 equals 'ABC'

```
      


#### See also: 

[lower_case](operators-i-to-m#lower_case), 
    	
----

[//]: # (keyword|operator_URL_file)
### `URL_file`

#### Possible use: 
  *  **`URL_file`** (`string`) --->  `file` 

#### Result: 
Constructs a file of type URL. Allowed extensions are limited to url
    	
----

[//]: # (keyword|operator_use_cache)
### `use_cache`

#### Possible use: 
  * `graph` **`use_cache`** `bool` --->  `graph`
  *  **`use_cache`** (`graph` , `bool`) --->  `graph` 

#### Result: 
if the second operand is true, the operand graph will store in a cache all the previously computed shortest path (the cache be cleared if the graph is modified).  

#### Comment: 
the operator alters the operand graph, it does not create a new one.    


#### See also: 

[path_between](operators-n-to-r#path_between), 
    	
----

[//]: # (keyword|operator_user_input)
### `user_input`

#### Possible use: 
  *  **`user_input`** (`any expression`) --->  `map<string,unknown>`
  * `string` **`user_input`** `any expression` --->  `map<string,unknown>`
  *  **`user_input`** (`string` , `any expression`) --->  `map<string,unknown>` 

#### Result: 
asks the user for some values (not defined as parameters). Takes a string (optional) and a map as arguments. The string is used to specify the message of the dialog box. The map is to specify the parameters you want the user to change before the simulation starts, with the name of the parameter in string key, and the default value as value.  

#### Comment: 
This operator takes a map [string::value] as argument, displays a dialog asking the user for these values, and returns the same map with the modified values (if any). The dialog is modal and will interrupt the execution of the simulation until the user has either dismissed or accepted it. It can be used, for instance, in an init section to force the user to input new values instead of relying on the initial values of parameters :

#### Examples: 
```
map<string,unknown> values <- user_input(["Number" :: 100, "Location" :: {10, 10}]); create bug number: int(values at "Number") with: [location:: (point(values at "Location"))]; map<string,unknown> values2 <- user_input("Enter numer of agents and locations",["Number" :: 100, "Location" :: {10, 10}]); create bug number: int(values2 at "Number") with: [location:: (point(values2 at "Location"))]; 

```
  
    	
----

[//]: # (keyword|operator_using)
### `using`

#### Possible use: 
  * `any expression` **`using`** `topology` --->  `unknown`
  *  **`using`** (`any expression` , `topology`) --->  `unknown` 

#### Result: 
Allows to specify in which topology a spatial computation should take place.

#### Special cases:     
  * has no effect if the topology passed as a parameter is nil

#### Examples: 
```
 
unknown var0 <- (agents closest_to self) using topology(world); // var0 equals the closest agent to self (the caller) in the continuous topology of the world

```
  
    	
----

[//]: # (keyword|operator_variance)
### `variance`

#### Possible use: 
  *  **`variance`** (`container`) --->  `float` 

#### Result: 
the variance of the elements of the operand. See <A href="http://en.wikipedia.org/wiki/Variance">Variance</A> for more details.  

#### Comment: 
The operator casts all the numerical element of the list into float. The elements that are not numerical are discarded.

#### Examples: 
```
 
float var0 <- variance ([4.5, 3.5, 5.5, 7.0]); // var0 equals 1.671875

```
      


#### See also: 

[mean](operators-i-to-m#mean), [median](operators-i-to-m#median), 
    	
----

[//]: # (keyword|operator_variance)
### `variance`

#### Possible use: 
  *  **`variance`** (`float`) --->  `float`
  *  **`variance`** (`int`, `float`, `float`) --->  `float` 

#### Result: 
Returns the variance from a standard deviation.
Returns the variance of a data sequence. That is (sumOfSquares - mean*sum) / size with mean = sum/size.
    	
----

[//]: # (keyword|operator_variance_of)
### `variance_of`

#### Possible use: 
  * `container` **`variance_of`** `any expression` --->  `unknown`
  *  **`variance_of`** (`container` , `any expression`) --->  `unknown` 

#### Result: 
the variance of the right-hand expression evaluated on each of the elements of the left-hand operand  

#### Comment: 
in the right-hand operand, the keyword each can be used to represent, in turn, each of the right-hand operand elements.    


#### See also: 

[min_of](operators-i-to-m#min_of), [max_of](operators-i-to-m#max_of), [sum_of](operators-s-to-z#sum_of), [product_of](operators-n-to-r#product_of), 
    	
----

[//]: # (keyword|operator_vertical)
### `vertical`

#### Possible use: 
  *  **`vertical`** (`msi.gama.util.GamaMap<java.lang.Object,java.lang.Integer>`) --->  `msi.gama.util.tree.GamaNode<java.lang.String>`
    	
----

[//]: # (keyword|operator_voronoi)
### `voronoi`

#### Possible use: 
  *  **`voronoi`** (`list<point>`) --->  `list<geometry>`
  * `list<point>` **`voronoi`** `geometry` --->  `list<geometry>`
  *  **`voronoi`** (`list<point>` , `geometry`) --->  `list<geometry>` 

#### Result: 
A list of geometries corresponding to the Voronoi diagram built from the list of points
A list of geometries corresponding to the Voronoi diagram built from the list of points according to the given clip

#### Examples: 
```
 
list<geometry> var0 <- voronoi([{10,10},{50,50},{90,90},{10,90},{90,10}]); // var0 equals the list of geometries corresponding to the Voronoi Diagram built from the list of points. 
list<geometry> var1 <- voronoi([{10,10},{50,50},{90,90},{10,90},{90,10}], square(300)); // var1 equals the list of geometries corresponding to the Voronoi Diagram built from the list of points with a square of 300m side size as clip.

```
  
    	
----

[//]: # (keyword|operator_weight_of)
### `weight_of`

#### Possible use: 
  * `graph` **`weight_of`** `unknown` --->  `float`
  *  **`weight_of`** (`graph` , `unknown`) --->  `float` 

#### Result: 
returns the weight of the given edge (right-hand operand) contained in the graph given in right-hand operand.  

#### Comment: 
In a localized graph, an edge has a weight by default (the distance between both vertices).

#### Special cases:     
  * if the left-operand (the graph) is nil, returns nil    
  * if the right-hand operand is not an edge of the given graph, weight_of checks whether it is a node of the graph and tries to return its weight    
  * if the right-hand operand is neither a node, nor an edge, returns 1.

#### Examples: 
```
graph graphFromMap <-  as_edge_graph([{1,5}::{12,45},{12,45}::{34,56}]);  
float var1 <- graphFromMap weight_of(link({1,5},{12,45})); // var1 equals 1.0

```
  
    	
----

[//]: # (keyword|operator_weighted_means_DM)
### `weighted_means_DM`

#### Possible use: 
  * `msi.gama.util.IList<java.util.List>` **`weighted_means_DM`** `msi.gama.util.IList<java.util.Map<java.lang.String,java.lang.Object>>` --->  `int`
  *  **`weighted_means_DM`** (`msi.gama.util.IList<java.util.List>` , `msi.gama.util.IList<java.util.Map<java.lang.String,java.lang.Object>>`) --->  `int` 

#### Result: 
The index of the candidate that maximizes the weighted mean of its criterion values. The first operand is the list of candidates (a candidate is a list of criterion values); the second operand the list of criterion (list of map)

#### Special cases:     
  * returns -1 is the list of candidates is nil or empty

#### Examples: 
```
 
int var0 <- weighted_means_DM([[1.0, 7.0],[4.0,2.0],[3.0, 3.0]], [["name"::"utility", "weight" :: 2.0],["name"::"price", "weight" :: 1.0]]); // var0 equals 1

```
      


#### See also: 

[promethee_DM](operators-n-to-r#promethee_dm), [electre_DM](operators-d-to-h#electre_dm), [evidence_theory_DM](operators-d-to-h#evidence_theory_dm), 
    	
----

[//]: # (keyword|operator_where)
### `where`

#### Possible use: 
  * `container` **`where`** `any expression` --->  `list`
  *  **`where`** (`container` , `any expression`) --->  `list` 

#### Result: 
a list containing all the elements of the left-hand operand that make the right-hand operand evaluate to true.  

#### Comment: 
in the right-hand operand, the keyword each can be used to represent, in turn, each of the right-hand operand elements.

#### Special cases:     
  * if the left-hand operand is a list nil, where returns a new empty list    
  * if the left-operand is a map, the keyword each will contain each value 
  
```
 
list var4 <- [1::2, 3::4, 5::6] where (each >= 4); // var4 equals [4, 6]
``` 



#### Examples: 
```
 
list var0 <- [1,2,3,4,5,6,7,8] where (each > 3); // var0 equals [4, 5, 6, 7, 8]  
list var2 <- g2 where (length(g2 out_edges_of each) = 0 ); // var2 equals [node9, node7, node10, node8, node11] 
list var3 <- (list(node) where (round(node(each).location.x) > 32); // var3 equals [node2, node3]

```
      


#### See also: 

[first_with](operators-d-to-h#first_with), [last_with](operators-i-to-m#last_with), [where](operators-s-to-z#where), 
    	
----

[//]: # (keyword|operator_with_lifetime)
### `with_lifetime`

#### Possible use: 
  * `predicate` **`with_lifetime`** `int` --->  `predicate`
  *  **`with_lifetime`** (`predicate` , `int`) --->  `predicate` 

#### Result: 
change the parameters of the given predicate

#### Examples: 
```
predicate with_lifetime 10 

```
  
    	
----

[//]: # (keyword|operator_with_max_of)
### `with_max_of`

#### Possible use: 
  * `container` **`with_max_of`** `any expression` --->  `unknown`
  *  **`with_max_of`** (`container` , `any expression`) --->  `unknown` 

#### Result: 
one of elements of the left-hand operand that maximizes the value of the right-hand operand  

#### Comment: 
in the right-hand operand, the keyword each can be used to represent, in turn, each of the right-hand operand elements.

#### Special cases:     
  * if the left-hand operand is nil, with_max_of returns the default value of the right-hand operand

#### Examples: 
```
 
unknown var0 <- [1,2,3,4,5,6,7,8] with_max_of (each ); // var0 equals 8 
unknown var2 <- g2 with_max_of (length(g2 out_edges_of each)  ) ; // var2 equals node4 
unknown var3 <- (list(node) with_max_of (round(node(each).location.x)); // var3 equals node3 
unknown var4 <- [1::2, 3::4, 5::6] with_max_of (each); // var4 equals 6

```
      


#### See also: 

[where](operators-s-to-z#where), [with_min_of](operators-s-to-z#with_min_of), 
    	
----

[//]: # (keyword|operator_with_min_of)
### `with_min_of`

#### Possible use: 
  * `container` **`with_min_of`** `any expression` --->  `unknown`
  *  **`with_min_of`** (`container` , `any expression`) --->  `unknown` 

#### Result: 
one of elements of the left-hand operand that minimizes the value of the right-hand operand  

#### Comment: 
in the right-hand operand, the keyword each can be used to represent, in turn, each of the right-hand operand elements.

#### Special cases:     
  * if the left-hand operand is nil, with_max_of returns the default value of the right-hand operand

#### Examples: 
```
 
unknown var0 <- [1,2,3,4,5,6,7,8] with_min_of (each ); // var0 equals 1 
unknown var2 <- g2 with_min_of (length(g2 out_edges_of each)  ); // var2 equals node11 
unknown var3 <- (list(node) with_min_of (round(node(each).location.x)); // var3 equals node0 
unknown var4 <- [1::2, 3::4, 5::6] with_min_of (each); // var4 equals 2

```
      


#### See also: 

[where](operators-s-to-z#where), [with_max_of](operators-s-to-z#with_max_of), 
    	
----

[//]: # (keyword|operator_with_optimizer_type)
### `with_optimizer_type`

#### Possible use: 
  * `graph` **`with_optimizer_type`** `string` --->  `graph`
  *  **`with_optimizer_type`** (`graph` , `string`) --->  `graph` 

#### Result: 
changes the shortest path computation method of the given graph  

#### Comment: 
the right-hand operand can be "Djikstra", "Bellmann", "Astar" to use the associated algorithm. Note that these methods are dynamic: the path is computed when needed. In contrarily, if the operand is another string, a static method will be used, i.e. all the shortest are previously computed.

#### Examples: 
```
graphEpidemio <- graphEpidemio with_optimizer_type "static"; 

```
      


#### See also: 

[set_verbose](operators-s-to-z#set_verbose), 
    	
----

[//]: # (keyword|operator_with_precision)
### `with_precision`

#### Possible use: 
  * `point` **`with_precision`** `int` --->  `point`
  *  **`with_precision`** (`point` , `int`) --->  `point`
  * `float` **`with_precision`** `int` --->  `float`
  *  **`with_precision`** (`float` , `int`) --->  `float`
  * `geometry` **`with_precision`** `int` --->  `geometry`
  *  **`with_precision`** (`geometry` , `int`) --->  `geometry` 

#### Result: 
Rounds off the ordinates of the left-hand point to the precision given by the value of right-hand operand
Rounds off the value of left-hand operand to the precision given by the value of right-hand operand
A geometry corresponding to the rounding of points of the operand considering a given precison.

#### Examples: 
```
 
point var0 <- {12345.78943, 12345.78943, 12345.78943} with_precision 2 ; // var0 equals {12345.79, 12345.79, 12345.79} 
float var1 <- 12345.78943 with_precision 2; // var1 equals 12345.79 
float var2 <- 123 with_precision 2; // var2 equals 123.00 
geometry var3 <- self with_precision 2; // var3 equals the geometry resulting from the rounding of points of the geometry with a precision of 0.1.

```
      


#### See also: 

[round](operators-n-to-r#round), 
    	
----

[//]: # (keyword|operator_with_values)
### `with_values`

#### Possible use: 
  * `predicate` **`with_values`** `map` --->  `predicate`
  *  **`with_values`** (`predicate` , `map`) --->  `predicate` 

#### Result: 
change the parameters of the given predicate

#### Examples: 
```
predicate with_values ["time"::10] 

```
  
    	
----

[//]: # (keyword|operator_with_weights)
### `with_weights`

#### Possible use: 
  * `graph` **`with_weights`** `map` --->  `graph`
  *  **`with_weights`** (`graph` , `map`) --->  `graph`
  * `graph` **`with_weights`** `list` --->  `graph`
  *  **`with_weights`** (`graph` , `list`) --->  `graph` 

#### Result: 
returns the graph (left-hand operand) with weight given in the map (right-hand operand).  

#### Comment: 
this operand re-initializes the path finder

#### Special cases:     
  * if the right-hand operand is a list, affects the n elements of the list to the n first edges. Note that the ordering of edges may change overtime, which can create some problems...    
  * if the left-hand operand is a map, the map should contains pairs such as: vertex/edge::double 
  
```
graph_from_edges (list(ant) as_map each::one_of (list(ant))) with_weights (list(ant) as_map each::each.food) 
``` 


    	
----

[//]: # (keyword|operator_without_holes)
### `without_holes`

#### Possible use: 
  *  **`without_holes`** (`geometry`) --->  `geometry` 

#### Result: 
A geometry corresponding to the operand geometry (geometry, agent, point) without its holes

#### Examples: 
```
 
geometry var0 <- solid(self); // var0 equals the geometry corresponding to the geometry of the agent applying the operator without its holes.

```
  
    	
----

[//]: # (keyword|operator_writable)
### `writable`

#### Possible use: 
  * `file` **`writable`** `bool` --->  `file`
  *  **`writable`** (`file` , `bool`) --->  `file` 

#### Result: 
Marks the file as read-only or not, depending on the second boolean argument, and returns the first argument  

#### Comment: 
A file is created using its native flags. This operator can change them. Beware that this change is system-wide (and not only restrained to GAMA): changing a file to read-only mode (e.g. "writable(f, false)")

#### Examples: 
```
 
file var0 <- shape_file("../images/point_eau.shp") writable false; // var0 equals returns a file in read-only mode

```
      


#### See also: 

[file](operators-d-to-h#file), 
    	
----

[//]: # (keyword|operator_xml_file)
### `xml_file`

#### Possible use: 
  *  **`xml_file`** (`string`) --->  `file` 

#### Result: 
Constructs a file of type xml. Allowed extensions are limited to xml
    	
----

[//]: # (keyword|operator_xor)
### `xor`

#### Possible use: 
  * `bool` **`xor`** `bool` --->  `bool`
  *  **`xor`** (`bool` , `bool`) --->  `bool` 

#### Result: 
a bool value, equal to the logical xor between the left-hand operand and the right-hand operand. False when they are equal  

#### Comment: 
both operands are always casted to bool before applying the operator. Thus, an expression like 1 xor 0 is accepted and returns true.    


#### See also: 

[or](operators-n-to-r#or), [and](operators-a-to-a#and), [!](operators-a-to-a#!), 
    	
----

[//]: # (keyword|operator_years_between)
### `years_between`

#### Possible use: 
  * `date` **`years_between`** `date` --->  `int`
  *  **`years_between`** (`date` , `date`) --->  `int` 

#### Result: 
Provide the exact number of years between two dates. This number can be positive or negative (if the second operand is smaller than the first one)

#### Examples: 
```
 
int var0 <- years_between(date('2000-01-01'), date('2010-01-01')); // var0 equals 10

```
  