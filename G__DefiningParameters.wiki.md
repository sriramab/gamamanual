# Defining Parameters (Under Construction)
<font color='red'><i>todo</i>:<br>
<ul><li>link with the UI (Parameters View)<br>
</li><li>improve this definition: add the different facets allowed (among, min, max, etc.)<br>
</li><li>be more precise about the vocabulary used (i.e. not "global variable" but "attribute of the simulation agent")<br>
</li><li>give different examples and constraints (not 2 parameters with the same name, not 2 with the same var).<br>
</font>
<hr /></li></ul>


<br />

Experiments can define input, i.e. parameters.
Defining parameters allows to make the value of a global variable definable by the user through the user graphic interface.

A parameter is defined as follow:

```
   parameter title var: global_var category: cat;
```

With:
  * title: string to display
  * var: reference to a global variable (defined in the global section)
  * category: string used to «store» the operators on the UI (optional)

Example:
```
   parameter "Value of toto: " var: toto;
```