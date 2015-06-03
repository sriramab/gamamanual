
# Defining Behaviors (Under Construction)
<font color='red'><i>todo</i>:<br>
<ul><li>give some insight on the execution order of reflexes<br>
</li><li>link to the built-in architectures<br>
</font>
<hr />
All agents (including the world and grid cells) are provided with a simple behavioral structure, based on reflexes. Species can define any number of reflexes within their body. In addition, all agents are provided with an init block that is activated at the creation of the agent is created.</li></ul>



## Table of contents 

* [Defining Behaviors (Under Construction)](#defining-behaviors-under-construction)
	* [reflex](#reflex)
	* [Init](#init)



## reflex

A reflex is a sequence of statements that can be executed, at each time step, by the agent. If no attribute when are defined, it will be executed every time step. If there is an facet **when**, it is executed only if the boolean expression evaluates to true. It is a convenient way to specify the behavior of the agents. Example:

```
reflex my_reflex { //Executed every time step
    write "Executing the unconditional reflex";
}
```

```
reflex my_reflex when: flip (0.5){ //Only executed when flip returns true
     write "Executing the conditional reflex";
}
```





## Init

A special form of reflex that is evaluated only once when the agent is created, after the initialization of its variables, and before it executes any reflex. Only one instance of init is allowed in each species (except in case of inheritance, see this section). Useful for creating all the agents of a model in the definition of the world, for instance. Example:

```
init { 
   color <- rnd_color(255);
}
```
