# Defining Inspectors and Monitors (Under Construction)

---


<br />

---

## Monitors
A monitor allows to follow the value of an arbitrary expression in GAML. It will appear, in the User Interface, in a small window on its own and be recomputed every time step (or according to its 'refresh\_every' facet).
Definition of a monitor:
```
monitor monitor_name value: an_expression refresh_every: nb_steps;
```
with:
  * value: mandatory, the expression whose value will be displayed by the monitor.
  * refresh\_every: int, optional : the number of simulation steps between two evaluations of the expression (default is 1).

Example:
```
  monitor "nb preys" value: length(prey as list);  
```
<br />

---

## Inspectors