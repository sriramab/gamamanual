
# Parameter Space

## Table of contents 

* [Parameter Space](#parameter-space)
	* [Parameter definition](#parameter-definition)
	* [The method element](#the-method-element)


## Parameter definition
The **parameter** elements specifies which model parameters will change through the successive simulations.
A parameter is defined as follows:
```
parameter title var: global_variable + possible_values
```

There are 2 ways to describe the range in which the value of the parameter will be explored  :
* Explicit list: **among**: values\_list
```
   parameter "Value of toto:" var: toto among: [1, 3, 7, 15, 100]; 
```
* Range : **min**: min\_value **max**: max\_value **step**: increment\_step
```
   parameter "Value of toto:" var: toto min: 1 max: 100 step: 2;
```

For Strings and Booleans, you can only use the Explicit List.

Each Batch methods may accept only some kind of definitions and parameter types. See the description of each of them for details.

## The method element
The optional method element controls the algorithm which drives the batch.

If this element is omitted, the batch will run in a classical way, changing one parameter value at each step until all the possible combinations of parameter values have been covered. See the Exhaustive exploration of the parameter space for more details.

When used, this element must contain at least a name attribute to specify the algorithm to use. It has theses facets:
* minimize or a maximize (mandatory for optimization method): a attribute defining the expression to be optimized.
* aggregation (optional): possible values ("min", "max"). Each combination of parameter values is tested **repeat** times. The aggregated fitness of one combination is by default the average of fitness values obtained with those repetitions. This facet can be used to tune this aggregation function and to choose to compute the aggregated fitness value as the minimum or the maximum of the obtained fitness values.
* other parameters linked to exploration method (optional) : see below for a description of these parameters.

Exemples of use of the method elements:
```
method exhaustive minimize: nb_infected ;

method genetic pop_dim: 3 crossover_prob: 0.7 mutation_prob: 0.1 nb_prelim_gen: 1 max_gen: 5  minimize: nb_infected aggregation: "max";
```