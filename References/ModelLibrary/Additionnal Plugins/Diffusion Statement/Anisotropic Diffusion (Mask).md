[//]: # (keyword|operator_as_matrix)
[//]: # (keyword|operator_hsb)
[//]: # (keyword|operator_column_at)
[//]: # (keyword|statement_diffuse)
[//]: # (keyword|type_matrix)
[//]: # (keyword|concept_matrix)
# Anisotropic diffusion with mask


_Author : Benoit Gaudou_

This model is used to show how an anisotropic diffusion can be used with a mask. The cell at the center of the grid emit a pheromon at each step, which is spread through the grid thanks to the diffusion mechanism. A mask is used to restrict the diffusion to a "corridor" (the white part of the bmp image)


Code of the model : 

```

model diffusion

global {
	int grid_size <- 51;
  	geometry shape <- envelope(square(grid_size) * 10);
  	cells selected_cells;
  	cells2 selected_cells2;
  	// Load the image mask as a matrix. The white part of the image is the part where diffusion will work, and the black part is where diffusion will be blocked.
  	matrix mymask <- file("../includes/mask3.bmp") as_matrix({grid_size,grid_size});
  	// Declare the anisotropic matrix (diffuse from the center)
  	matrix<float> math_diff <- matrix([
									[1/9,1/9,1/9],
									[1/9,1/9,1/9],
									[1/9,1/9,1/9]]);
	// Initialize the emiter cell as the cell at the center of the word
	init {
		selected_cells <- location as cells;
		selected_cells2 <- location as cells2;
	}
	reflex new_Value when: cycle=2 {
		ask selected_cells  {
			phero <- 1.0;
		}
		ask selected_cells2 {
			phero <- 1.0;
		}
	}
	
	reflex print_total_phero {
		float total <-0.0;
		ask cells {
			total <- total + phero;
		}
		write total;
	}

	reflex diff {
		// Declare a diffusion on the grid "cells". The value of the diffusion will be store in the new variable "phero" of the cell.
		diffuse var: phero on: cells matrix: math_diff mask: mymask keep_masked_cells_null: false conserve_value:true method:convolution;	
//		diffuse var: phero on: cells2 matrix: math_diff mask: mymask keep_masked_cells_null: true conserve_value:true method:convolution;
	}
}


grid cells height: grid_size width: grid_size {
	// "phero" is the variable storing the value of the diffusion
	float phero <- 0.0;
	bool ismasked <- false;
	// the color of the cell is linked to the value of "phero".
	rgb color <- hsb(phero,1.0,1.0) update: ismasked ? #black : hsb(phero,1.0,1.0);
	init {
			if ( ((mymask column_at grid_x) at grid_y) != -1) {
				ismasked <-true;
		}
	}
	// Update the "grid_value", which will be used for the elevation of the cell
	float grid_value update: ismasked ? 100 : min([100, phero * 100]);
}

grid cells2 height: grid_size width: grid_size {
	// "phero" is the variable storing the value of the diffusion
	float phero <- 0.0;
	bool ismasked <- false;
	// the color of the cell is linked to the value of "phero".
	rgb color <- hsb(phero,1.0,1.0) update: ismasked ? #black : hsb(phero,1.0,1.0);
	init {
			if ( ((mymask column_at grid_x) at grid_y) != -1) {
				ismasked <-true;
		}
	}
	// Update the "grid_value", which will be used for the elevation of the cell
	float grid_value update: ismasked ? 100 : min([100, phero * 100]);
}


experiment diffusion type: gui {
	output {
		display a type: opengl {
			// Display the grid with elevation
			grid cells elevation: true triangulation: true;
		}
		display b type: opengl {
			// Display the grid with elevation
			grid cells2 elevation: true triangulation: true;
		}
	}
}
```
