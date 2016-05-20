# Extension

----

 simtools.gamanalyzer.fr

## Table of Contents
### Operators


### Statements
[analyse](#analyse), 

### Skills


### Architectures



### Species
[agent_group_follower](#agent_group_follower), [AgGroupAnalizer](#aggroupanalizer), [cluster_builder](#cluster_builder), 


----

## Operators
	

----

## Skills
	

----

## Statements
	

----

[//]: # (keyword|statement_analyse)
### analyse 
#### Facets 
  
  * **`species_to_analyse`** (any type in [string, string]), (omissible) :   
  * **`with_constraint`** (any type in [string, string]): 

#### Embedments
* The `analyse` statement is of type: **Single statement**
* The `analyse` statement can be embedded into: experiment, 
* The `analyse` statement embeds statements: 

[Top of the page](#table-of-contents)
		
		
	
----

## Species
	
    	
----

[//]: # (keyword|species_agent_group_follower)
## `agent_group_follower`	

### Actions
	  
	 
#### **`analyse_cluster`**

* returns: `void`
 			
* → **`species_to_analyse`** (`string`):   
	 
#### **`at_cycle`**

* returns: `list`
 			
* → **`with_matrix`** (`string`):  			
* → **`with_var`** (`string`):   
	 
#### **`at_var`**

* returns: `list`
 			
* → **`with_matrix`** (`string`):  			
* → **`with_var`** (`string`):   
	 
#### **`distrib_legend`**

* returns: `list`
 			
* → **`with_var`** (`string`): 			

[Top of the page](#table-of-contents) 
	
    	
----

[//]: # (keyword|species_AgGroupAnalizer)
## `AgGroupAnalizer`	

### Actions
	  
	 
#### **`creation_cluster`**

* returns: `void`
			

[Top of the page](#table-of-contents) 
	
    	
----

[//]: # (keyword|species_cluster_builder)
## `cluster_builder`	

### Actions
	  
	 
#### **`clustering_cobweb`**

* returns: `list<list<agent>>`
  
	 
#### **`clustering_DBScan`**

* returns: `list<list<agent>>`
  
	 
#### **`clustering_em`**

* returns: `list<list<agent>>`
  
	 
#### **`clustering_farthestFirst`**

* returns: `list<list<agent>>`
  
	 
#### **`clustering_simple_kmeans`**

* returns: `list<list<agent>>`
 			
* → **`agents`** (`list`):  			
* → **`attributes`** (`list`):  			
* → **`distance_f`** (``):  			
* → **`dont_replace_missing_values`** (``):  			
* → **`max_iterations`** (``):  			
* → **`num_clusters`** (``):  			
* → **`preserve_instances_order`** (``):  			
* → **`seed`** (``):   
	 
#### **`clustering_xmeans`**

* returns: `list<list<agent>>`
 			
* → **`agents`** (`list`):  			
* → **`attributes`** (`list`):  			
* → **`bin_value`** (`float`): value that represents true in the new attributes 			
* → **`cut_off_factor`** (`float`): the cut-off factor to use 			
* → **`distance_f`** (`string`): The distance function to use. 4 possible distance functions: euclidean (by default) ; 'chebyshev', 'manhattan' or 'levenshtein' 			
* → **`max_iterations`** (`int`): the maximum number of iterations to perform 			
* → **`max_kmeans`** (`int`): the maximum number of iterations to perform in KMeans 			
* → **`max_kmeans_for_children`** (`int`): the maximum number of iterations KMeans that is performed on the child centers 			
* → **`max_num_clusters`** (`int`): the maximum number of clusters 			
* → **`min_num_clusters`** (`int`): the maximum number of clusters 			
* → **`seed`** (`int`): random number seed to be used			

[Top of the page](#table-of-contents) 
	
	
----

## Architectures 
	