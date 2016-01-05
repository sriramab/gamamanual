# Defining monitors and inspectors

Other outputs can be very useful to study better the behavior of your agents.

## Index

* [Define a monitor](#define-a-monitor)
* [Define an inspector](#define-an-inspector)

## Define a monitor

A monitor allows to follow the value of an arbitrary expression in GAML. It will appear, in the User Interface, in a small window on its own and be recomputed every time step (or according to its refresh facet). Definition of a monitor: 

monitor monitor_name value: an_expression refresh:boolean_statement;

with:
* value: mandatory, the expression whose value will be displayed by the monitor.
* refresh: bool statement, optional : the new value is computed if the bool statement returns true.

Example:

```
experiment my_experiment type: gui {
	output {
		monitor monitor_name value: cycle refresh:every(1);
	}
}
```

NB : you can also declare monitors during the simulation, by clicking on the button "Add new monitor", and specifying the name of the variable you want to follow.

## Define an inspector

During the simulation, the user interface of GAMA provides the user the possibility to inspect an agent, or a group of agents (see this [page] to learn more about this). But you can also define the inspector you want directly from your model, as an output of the experiment.

Use the statement inspect to define your inspector. The inspector has to be named (using the facet "name"), a value has to be specified (with the value facet)

[TODO quand corrig�]