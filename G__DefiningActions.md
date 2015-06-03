
# Defining Actions (Under Construction)
<font color='red'><i>todo</i>:<br>
<ul><li>give more examples of various action calls and definitions<br>
</li><li>make a complete section on primitives (and how they handle their arguments)<br>
</font>
<hr />
An action is a capability available to the agents of a species (what they can do). It is a block of statements that can be used and reused whenever needed.<br>
An action can accept arguments. An action can return a result (statement <b>return</b>).</li></ul>


## Table of contents 

* [Defining Actions (Under Construction)](#defining-actions-under-construction)
	* [Declaring Actions](#declaring-actions)
	* [Calling Actions](#calling-actions)




## Declaring Actions

From a general point of view, an action is declared with:
```
return_type action_name (var_type arg_name,...)  {
  [sequence_of_statements]
  [return value;]
}
```

If an action does not return a value, the keyword **action** is to be used instead of the **return\_type**.

```
action dummy_void {
    write "dummy_void";
}

action dummy_void_arg(int c) {
    write "dummy_void: " + c;
}

//in this action, the argument *a* could be omitted when calling the action (and will have *100* for default value)
int dummy_return (int a <- 100, int b) {
    return a + b;
}
```

Some actions, called primitives, are directly coded in Java : for instance, the write action defined for all the agents.





## Calling Actions

There are two ways to call an action: using a statement or as part of an expression
  * action that does not return a result:
```
do dummy_void;
do dummy_void_arg(10);
```
  * action that returns a result:
```
my_var <- dummy_return (10, 50);
my_var <- dummy_return (a: 10, b: 50);
my_var <- dummy_return (b: 50);
```

It is possible to precise the agent that is calling the action:
```
my_var <- self dummy_return (10, 50);
```
The **self** keyword denotes the agent that will execute the action (the action must be defined in its species).
