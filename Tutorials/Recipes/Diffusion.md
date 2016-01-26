
# Implementing diffusions

GAMA provides you the possibility to represent and simulate a diffusion through a grid topology. 

## Index

* [Diffusion statement](#diffusion-statement)
* [Diffusion with matrix](#diffusion-with-matrix)
* [Diffusion with parameters](#diffusion-with-parameters)

## Diffusion statement

The statement to use for the diffusion is `diffusion`. It has to be used in a `grid` species. The `diffusion` uses the following facets:

* **`var`** : the name of the variable that will be diffused through the grid. This variable has to be declared as an attribute of the grid.
* **`on`** : the list of agents (usually the entire grid) where the diffusion will occur.
* `cycle_length`(int) : the number of diffusion operation applied in one simulation step.
* `mask`(matrix): a matrix masking the diffusion (matrix created from a image for example)

cycle_length (int): the number of diffusion operation applied in one simulation step
mask (matrix): a matrix masking the diffusion (matrix created from a image for example)
mat_diffu (matrix): the diffusion matrix (can have any size)
method (an identifier), takes values in: {convolution, dot_product}: the diffusion method
proportion (float): a diffusion rate
radius (int): a diffusion radius