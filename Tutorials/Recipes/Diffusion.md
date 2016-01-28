
# Implementing diffusions

GAMA provides you the possibility to represent and simulate a diffusion through a grid topology. 

## Index

* [Diffusion statement](#diffusion-statement)
* [Diffusion with matrix](#diffusion-with-matrix)
* [Diffusion with parameters](#diffusion-with-parameters)
* [Using mask](#using-mask)

## Diffusion statement

The statement to use for the diffusion is `diffusion`. It has to be used in a `grid` species. The `diffusion` uses the following facets:

* **`var`** : the name of the variable that will be diffused through the grid. This variable has to be declared as an attribute of the grid.
* **`on`** : the list of agents (usually the entire grid) where the diffusion will occur.
* `cycle_length` (int): the number of diffusion operation applied in one simulation step.
* `mat_diffu` (matrix): the diffusion matrix.
* `mask` (matrix): a matrix masking the diffusion (matrix created from a image for example). The cells corresponding to the values smaller than "-1" in the mask matrix will not diffuse, and the other will diffuse.
* `method` takes values in: {convolution, dot_product}: the diffusion method
* `proportion` (float): a diffusion rate (the default value is 1.0)
* `radius` (int): a diffusion radius (the default value is 1)
* `variation` (float): an absolute decrease of intensity that occurs between each place. It should be a positive number. (the default value is 1.0)

To write a diffusion, you first have to declare a grid, and declare a special attribute for the diffusion. You will then have to write the `diffusion` statement in an other scope (such as the `global` scope for instance), which will permit the values to be diffused at each step. There, you will specify which variable you want to diffuse (through the **`var`** facet), on which species or list of agents you want the diffusion (through the **`on`** facet), and how you want this value to be diffused (through all the other facets, we will see how it works [with matrix](#diffusion-with-matrix) and [with special parameters](#diffusion-with-parameters) just after).

Here is the template of code we will use for the next following part of this page:

```
global {
	int size <- 64; // the size has to be a power of 2.
  	cells selected_cells;

	// Initialize the emiter cell as the cell at the center of the word
	init {
		selected_cells <- location as cells;
	}
	// Affecting "1" to each step
	reflex new_Value {
		ask(selected_cells){
			phero <- 1.0;
		}	
	}

	reflex diff {
		// Declare a diffusion on the grid "cells" and on "quick_cells". The diffusion declared on "quick_cells" will make 10 computations at each step to accelerate the process. 
		// The value of the diffusion will be store in the new variable "phero" of the cell.
		diffusion var: phero on: cells /*HERE WRITE DOWN THE DIFFUSION PROPERTIES*/;			
	}
}


grid cells height: size width: size {
	// "phero" is the variable storing the value of the diffusion
	float phero  <- 0.0;
	// The color of the cell is linked to the value of "phero".
	rgb color <- hsb(phero,1.0,1.0) update: hsb(phero,1.0,1.0);
}


experiment diffusion type: gui {
	output {
		display a type: opengl {
			// Display the grid with elevation
			grid cells elevation: phero * 10 triangulation: true;
		}
	}
}
```

This model will simulate a diffusion through a grid at each step, affecting 1 to the center cell diffusing variable value. The diffusion will be seen during the simulation through a color code, and through the elevation of the cell.

## Diffusion with matrix

A first way of specifying the behavior of your diffusion is using diffusion matrix. A diffusion matrix is a 2 dimension matrix `[n][m]` with `float` values, where both `n` and `m` have to be **pair values**. The most often, diffusion matrix are square matrix, but you can also declare rectangular matrix.

Example of matrix:

```
matrix<float> mat_diff <- matrix([
		[1/9,1/9,1/9],
		[1/9,1/9,1/9],
		[1/9,1/9,1/9]]);
```

In the `diffusion` statement, you than have to specify the matrix of diffusion you want in the facet `mat_diffu`.

```
diffusion var: phero on: cells mat_diffu:mat_diff;
```

Using the facet `propagation`, you can specify if you want the value to be propagated as a _diffusion_ or as a _gratient_.

### Diffusion matrix

A _diffusion_ (the default value of the facet `propagation`) will spread the values to the neighbors cells according to the diffusion matrix, and all those values will be added together, as it is the case in the following example :

![resources/images/recipes/diffusion_computation.png](resources/images/recipes/diffusion_computation.png)

Note that the sum of all the values diffused at the next step is equal to the sum of the values that will be diffused multiply by the sum of the values of the diffusion matrix. That means that if the sum of the values of your diffusion matrix is larger than 1, the values will increase exponentially at each step. The sum of the value of a diffusion matrix is usually equal to 1.

Here are some example of matrix you can use, played with the template model:

![resources/images/recipes/uniform_diffusion.png](resources/images/recipes/uniform_diffusion.png)

![resources/images/recipes/anisotropic_diffusion.png](resources/images/recipes/anisotropic_diffusion.png)

### Gradient matrix

A `gradient` (use facet : `propagation:gradient`) is an other type of propagation. This time, only the larger value diffused will be chosen as the new one.

![resources/images/recipes/gradient_computation.png](resources/images/recipes/gradient_computation.png)

Note that unlike the _diffusion_ propagation, the sum of your matrix can be greater than 1 (and it is the case, most often !).

Here are some example of matrix with gradient propagation:

![resources/images/recipes/uniform_gradient.png](resources/images/recipes/uniform_gradient.png)

![resources/images/recipes/irregular_gradient.png](resources/images/recipes/irregular_gradient.png)

### Compute several propagations at the same step

You can compute several times the propagation you want by using the facet `cycle_length`. GAMA will compute for you the corresponding new matrix, and will apply it.

![resources/images/recipes/cycle_length.png](resources/images/recipes/cycle_length.png)

Writing those two thinks are exactly equivalent (for diffusion):

```
	matrix<float> mat_diff <- matrix([
			[1/81,2/81,3/81,2/81,1/81],
			[2/81,4/81,6/81,4/81,2/81],
			[3/81,6/81,1/9,6/81,3/81],
			[2/81,4/81,6/81,4/81,2/81],
			[1/81,2/81,3/81,2/81,1/81]]);
	reflex diff {
		diffusion var: phero on: cells mat_diffu:mat_diff;
```
```
	matrix<float> mat_diff <- matrix([
			[1/9,1/9,1/9],
			[1/9,1/9,1/9],
			[1/9,1/9,1/9]]);
	reflex diff {
		diffusion var: phero on: cells mat_diffu:mat_diff cycle_length:2;
```

### Executing several diffusion matrix

If you execute several times the statement `diffusion` with different matrix on the same variable, their values will be added (and centered if their dimension is not equal).

Thus, the following 3 matrix will be combined to create one unique matrix:

![resources/images/recipes/addition_matrix.png](resources/images/recipes/addition_matrix.png)

## Diffusion with parameters

Sometimes writing diffusion matrix is not exactly what you want, and you may prefer to just give some parameters to compute the correct diffusion matrix. You can use the following facets in order to do that : `propagation`, `variation` and `radius`.

Depending on which `propagation` you choose, and how many neighbors your grid have, the propagation matrix will be compute differently. The propagation matrix will have the size : range*2+1.

Let's note **P** for the propagation value, **V** for the variation, **R** for the range and **N** for the number of neighbors.

* **With diffusion propagation**

For diffusion propagation, we compute following the following steps:

(1) We determine the "minimale" matrix according to N (if N = 8, the matrix will be `[[P/9,P/9,P/9][P/9,1/9,P/9][P/9,P/9,P/9]]`. if N = 4, the matrix will be `[[0,P/5,0][P/5,1/5,P/5][0,P/5,0]]`).

(2) If R != 1, we propagate the matrix R times to obtain a `[2*R+1][2*R+1]` matrix (same computation as for `cycle_length`).

(3) If V != 0, we substract each value by V*DistanceFromCenter (DistanceFromCenter depends on N).

Ex with the default values (P=1, R=1, V=0, N=8):

* **With gradient propagation**

The value of each cell will be equal to **P/POW(N,DistanceFromCenter)-DistanceFromCenter*V**. (DistanceFromCenter depends on N).

Ex with R=2, other parameters default values (R=2, P=1, V=0, N=8):

![resources/images/recipes/gradient_computation_from_parameters.png](resources/images/recipes/gradient_computation_from_parameters.png)

Note that if you declared a diffusion matrix, you cannot use those 3 facets (it will raise a warning). Note also that if you use parameters, you will only have uniform matrix.

## Using mask

### Generalities

If you want to propagate some values in an heterogeneous grid, you can use some mask to forbid some cells to propagate their values.

You can pass a matrix to the facet `mask`. All the values smaller than `-1` will not propagate, and all the values greater or equal to `-1` will propagate.

A simple way to use mask is by loading an image :

![resources/images/recipes/simple_mask.png](resources/images/recipes/simple_mask.png)

Note that when you use the `on` facet for the `diffusion` statement, you can choose only some cells, and not every cells. In fact, when you restrain the values to be diffuse, it is exactly the same process as if you were defining a mask.

![resources/images/recipes/mask_with_on_facet.png](resources/images/recipes/mask_with_on_facet.png)

### Tips

Masks can be used to simulate a lot of environments. Here are some ideas for your models:

#### Wall blocking the diffusion

If you want to simulate a wall blocking a uniform diffusion, you can declare a second diffusion matrix that will be applied only on the cells where your wall will be. This diffusion matrix will "push" the values outside from himself, but conserving the values (the sum of the values of the diffusion still have to be equal to 1) :

```
matrix<float> mat_diff <- matrix([
			[1/9,1/9,1/9],
			[1/9,1/9,1/9],
			[1/9,1/9,1/9]]);
								
matrix<float> mat_diff_left_wall <- matrix([
			[0.0,0.0,2/9],
			[0.0,0.0,4/9],
			[0.0,0.0,2/9]]);

reflex diff { 
	diffusion var: phero on: (cells where(each.grid_x>30)) mat_diffu:mat_diff;
	diffusion var: phero on: (cells where(each.grid_x=30)) mat_diffu:mat_diff_left_wall;
}
```

![resources/images/recipes/wall_simulation.png](resources/images/recipes/wall_simulation.png)

#### Wind pushing the diffusion

Let's simulate a uniform diffusion that is pushed by a wind from "north" everywhere in the grid. A wind from "west" as blowing at the top side of the grid. We will here have to build 2 matrix : one for the uniform diffusion, one for the "north" wind and one for the "west" wind. The sum of the values for the 2 matrix meant to simulate the wind will be equal to 0 (as it will be add to the diffusion matrix).

```
matrix<float> mat_diff <- matrix([
		[1/9,1/9,1/9],
		[1/9,1/9,1/9],
		[1/9,1/9,1/9]]);
								
matrix<float> mat_wind_from_west <- matrix([
		[-1/9,0.0,1/9],
		[-1/9,0.0,1/9],
		[-1/9,0.0,1/9]]);
								
matrix<float> mat_wind_from_north <- matrix([
		[-1/9,-1/9,-1/9],
		[0.0,0.0,0.0],
		[1/9,1/9,1/9]]);

reflex diff { 
	diffusion var: phero on: cells mat_diffu:mat_diff;
	diffusion var: phero on: cells mat_diffu:mat_wind_from_north;
	diffusion var: phero on: (cells where (each.grid_y>=32)) mat_diffu:mat_wind_from_west;
}
```

![resources/images/recipes/diffusion_with_wind.png](resources/images/recipes/diffusion_with_wind.png)

#### Endless world

Note that when your world is not a torus, it has the same effect as a _mask_, since all the values outside from the world cannot diffuse some values back :

![resources/images/recipes/uniform_diffusion_near_edge.png](resources/images/recipes/uniform_diffusion_near_edge.png)

You can "fake" the fact that your world is endless by adding a different diffusion for the cells with `grid_x=0` to have almost the same result :

![resources/images/recipes/uniform_diffusion_near_edge_with_mask.png](resources/images/recipes/uniform_diffusion_near_edge_with_mask.png)

```
matrix<float> mat_diff <- matrix([
			[1/9,1/9,1/9],
			[1/9,1/9,1/9],
			[1/9,1/9,1/9]]);
								
matrix<float> mat_diff_upper_edge <- matrix([
			[0.0,0.0,0.0],
			[1/9+7/81,2/9+1/81,1/9+7/81],
			[1/9,1/9,1/9]]);

reflex diff { 
	diffusion var: phero on: (cells where(each.grid_y>0)) mat_diffu:mat_diff;
	diffusion var: phero on: (cells where(each.grid_y=0)) mat_diffu:mat_diff_upper_edge;
}
```