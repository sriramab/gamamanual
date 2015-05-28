# Defining Attributes (Under Construction)
<font color='red'><i>todo</i>:<br>
<ul><li>move temp variables elsewhere<br>
</li><li>rewrite "Reserved Keywords" (as most of the rules are now obsolete)<br>
</li><li>remove the 'type' subsection as it is now obsolete as well<br>
</li><li>link to data types for the default values<br>
</li><li>add a paragraph on systematic casting (with examples)<br>
</font>
<hr />
Attributes define the internal state of the agents of the species.</li></ul>







## Attribute Declaration
An attribute is declared using the following syntax:

```
datatype var_name [optional_facets: ...];
```

In this declaration, datatype refers to the name of a built-in type or a species declared in the model. The value of `var_name` can be any combination of letters and digits (plus the underscore, "`_`") that does not begin with a digit and that follows certain rules (see "Naming variables"). Examples of valid declarations are:

```
int i;
list my_list;
my_species_name an_agent_of_my_species; // if my_species is declared in the model as a species.
```

These attributes are given default values at their creation, depending on their datatype:
Default Value
| **int** | **float** | **bool** | **string** | **list** | **matrix** | **point** | **rgb** | **graph** | **geometry** |
|:--|:-|:|:--|:|:--|:-|:--|:-|:-|
| 0       | 0.0       | false    | ''         | [ ]      | nil        | nil       | black   | nil       | nil          |


#### init or <-
When it is necessary to initialize the attribute with another value than its default value, the init (or <-) facet can be used.

```
datatype var_name <- initial_expression [optional_attributes:...];
```

The `initial_expression` is expected to be of the same type as the attribute (otherwise it is casted to the datatype). Its only (obvious) restriction is that it cannot refer to the attribute being declared. Examples of valid declarations are:

```
int i <- 0;
list my_list <- [i + 1, i + 2, i + 3];
agent an_agent <- self;
```

#### const
If the value of the attribute is not intended to change over time, it is preferable to declare it as a constant in order to avoid any surprise (and to optimize, a little bit, the compiler's work). This is done with the const facet:

```
const var_name type: datatype <- initial_expression [optional_attributes:...];
```

With this declaration, the attribute var\_name will keep the result of initial\_expression as its value for the whole execution of the simulation.

#### update

What if, on the contrary, the value of the attribute is supposed to change over time and the modeler wants to define this evolution? The `update` facet is precisely available for this purpose. Basically, its contents is evaluated every time step and assigned to the variable. It means that, unless the contents of this attribute refers to the attribute itself, every modification made in the model to the value of the attribute will be lost and replaced with the evaluation of the expression.

```
datatype var_name <- initial_expression update: value_expression [optional_attributes:...];
```

All the attributes of all the agents are updated at the same time, before they are given a chance to execute behaviors. Some examples of use for value:

  * Automatically evolving attributes:

```
int my_int <- 0 update: my_int + 1: // -> my_int is incremented by 1 every time step.
float my_float <- 100 update: my_float - (my_float / 100); // -> my_float is decremented by 1% every time step.
```

  * Sticky attributes:

```
int sticky_int update: 100; // -> whatever the changes made in the model to sticky_int, its value returns to 100 at the beginning of every step.
```

  * Conditionally evolving attributes:

```
int cond_int update: (my_int < 100) ? 0 : my_int / 10; // -> the value of cond_int depends on that of my_int.
float log_my_int update: ln (my_int); // -> the value of "cond_int" is always coupled to that of my_int. 
```

### Special facets

#### function

The `update` facet is computed only every step. But sometimes, we need more accurate updates (i.e. that the value of the attribute be evaluated each time we use it).
The `function` facet has been introduced to this purpose and has the following syntax:
```
type1 var1 function: {an_expression} [optional_attributes:...];
```

Once a function is declared, whenever the attribute is used somewhere, the function is computed (so the value of the attribute always remains accurate).
The declaration of `function` is **incompatible** with both `init` or `update` (an error will be raised).
A shortcut has also been introduced:
```
type1 var1 -> {an_expression} [optional_attributes:...];
```

#### max, min
These two facets are only available in the context of int or float attributes. They allow the modeler to control the values of the attribute, by specifying a maximum and minimum value. The attribute will never be allowed to be lower than the minimum or greater than the maximum.

```
int max_energy <- 300 min: 100 max: 3000;
```

min and max combine gracefully with the parameter facet and allow to control what the user can enter, or the limits between which exploring the values of variables.


#### 

<\_type\_>



Only defined in the context of containers: matrix, list, map and graph attributes. Allows to define the type/species of values contained in the container. For instance, it can be handy, sometimes, to fix the species of the agents in a list at once rather than having to use the of\_species operator every time. An example of that with the re-declaration of the built-in neighbours variable in a model with only one species of agents:

```
list<bug> neighbours;
```

Doing so enables the use of neighbours, in the following expressions, without having to specify which kind of agents are manipulated in it.

### Temporary variable
A temporary variable (or local variable) is a variable that has an existence only in a statement block: as soon as the end of the block, the variable is deleted from the computer memory. It is local to the scope in which it is defined. The naming rules follow those of the variable declarations. In addition, a temporary variable cannot be declared twice in the same scope. The generic syntax is:

```
datatype temp_var1 <- an_expression;
```

After it has been declared this way, a temporary variable can be used like regular variables (for instance, the `<-` statement should be used to assign it a new value within the same scope).





## Naming variables

### Reserved Keywords
In GAML, some keywords are already reserved with a specific meaning and cannot be used for naming variables (and also species, actions, etc. ). They are :
  * The names of the global built-in variables
  * The names of the primitive data types and new species defined in the model.
  * The special keywords used by the language.
  * The names of the variables found in every species.
  * The names of the variables defined in skills when a species declares their use.
  * The names of the units that can attached to numeric values.

### Naming conventions
A variable name can be sequence of alphanumeric characters (plus the underscore, "`_`"). It should follow certain rules:
  * it should not begin by a digit;
  * it should not contain space characters.

By convention, it is recommended that:
  * variable name begins by a lower case letter.