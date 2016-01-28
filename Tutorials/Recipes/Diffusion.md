
# Implementing diffusions

GAMA provides you the possibility to represent and simulate a diffusion through a grid topology. 

## Index

* [Diffusion statement](#diffusion-statement)
* [Diffusion with matrix](#diffusion-with-matrix)
* [Diffusion with parameters](#diffusion-with-parameters)
* [Further specifications for diffusion](#further-specifications-for-diffusion)
* [Diffusion and performance](#diffusion-and-performance)

## Diffusion statement

The statement to use for the diffusion is `diffusion`. It has to be used in a `grid` species. The `diffusion` uses the following facets:

* **`var`** : the name of the variable that will be diffused through the grid. This variable has to be declared as an attribute of the grid.
* **`on`** : the list of agents (usually the entire grid) where the diffusion will occur.
* `cycle_length` (int): the number of diffusion operation applied in one simulation step.
* `mat_diffu` (matrix): the diffusion matrix.
* `mask` (matrix): a matrix masking the diffusion (matrix created from a image for example). The cells corresponding to the values smaller than "-1" in the mask matrix will not diffuse, and the other will diffuse.
* `method` takes values in: {convolution, dot_product}: the diffusion method
* `proportion` (float): a diffusion rate
* `radius` (int): a diffusion radius
* `variation` (float): an absolute decrease of intensity that occurs between each place. It should be a positive number.

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
matrix<float> math_diff <- matrix([
		[1/9,1/9,1/9],
		[1/9,1/9,1/9],
		[1/9,1/9,1/9]]);
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

## Diffusion with parameters

## Further specifications for diffusion

## Diffusion and performance