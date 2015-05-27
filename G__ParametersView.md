# Parameters View

---

In the case of an [experiment](G__DefiningExperiments.md), the modeler can [define the parameters](G__DefiningParameters.md) he wants to be able to modify to explore the simulation, and thus the ones he wants to be able to display and alter in the GUI interface.

**It important to notice that all modification made in the parameters are used for simulation reload only. Creation of a new simulation from the model will erase the modifications.**


<br />

---

## Built-in parameters
Every [GUI experiment](G__DefiningExperiments.md) displays a pane named "Parameters" containing at least two built-in parameters related to the random generator:
  * the Random Number Generator, with a choice between 4 RNG implementations,
  * the Random Seed

<br />
<img src='images/experiments/parameters_built_in.png' /> <br />

<br />

---

## Parameters View
The modeler can [define himself parameters](G__DefiningParameters.md) that can be displayed in the GUI and that are sorted by categories. Note that the interface will depend on the data type of the parameter: for example, for integer or float parameters, a simple text box will be displayed whereas a color selector will be available for color parameters. The parameters value displayed are the initial value provided to the variables associated to the parameters in the model.

<br />
<img src='images/experiments/parameters.png' /> <br />

The above parameters view is generated from the following code:
```
experiment maths type: gui {
	parameter "my_integer" var: i <- 0 category:"Simple types";
	parameter "my_float" var: f <- 0.0 category:"Simple types";
	parameter "my_string" var: s <- "" category:"Simple types";

	parameter "my_list" var: l <- [] category:"Complex types";
	parameter "my_matrix" var: m <- matrix([[1,2],[3,4]]) category:"Complex types";
	parameter "my_pair" var: p <- 3::5 category:"Complex types";
	parameter "my_map" var: mp <- ["a"::4] category:"Complex types";
	parameter "my_color" var: c <- #green category:"Complex types";

	output { ...  }
}
```
Click on Edit button in case of list or map parameters or the color or matrix will open an additional window to modify the parameter value.

<br />

---

## Modification of parameters values

The modeler can modify the parameters value (1 in the image below). In order that the modification to be taken into account in the simulation, he has to reload the simulation (click on the reload button, 2 in the image).
If he wants to come back to the initial value of parameters, he can click on the top-right curved arrow of the parameters view (cf. 3 in the image).


<br />
<img src='images/experiments/parameters_modifications.png' /> <br />