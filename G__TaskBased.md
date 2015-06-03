
# Task Based

GAMA integrated several task-based control architectures. Species can define any number of tasks within their body. At any given time, only one or several tasks are executed according to the architecture chosen:
  * **weighted\_tasks** : in this architecture, only the task with the maximal weight is executed.
  * **sorted\_tasks** : in this architecture, the tasks are all executed in the order specified by their weights (biggest first)
  * **probabilistic\_tasks**: this architecture uses the weights as a support for making a weighted probabilistic choice among the different tasks. If all tasks have the same weight, one is randomly chosen each step.


## Table of contents 

* [Task Based](#task-based)
	* [Declaration](#declaration)
	* [Task](#task)
		* [Sub elements](#sub-elements)
		* [Definition](#definition)


## Declaration


Using the Task architectures for a species require to use the **control** facet:

```
species dummy control: weighted_tasks {
   ...
}
```


```
species dummy control: sorted_tasks {
   ...
}
```


```
species dummy control: probabilistic_tasks {
   ...
}
```





## Task

### Sub elements
Besides a sequence of statements like reflex, a task contains the following sub elements:
  * weight: Mandatory. The priority level of the task.

### Definition
As reflex, a task is a sequence of statements that can be executed, at each time step, by the agent. If an agent owns several tasks, the scheduler chooses a task to execute based on its current priority weight value.


For example, consider the following example:
```
species dummy control: weighted_tasks {   
	task task1 weight: cycle mod 3 { 
		write string(cycle) + ":" + name + "->" + "task1";
	}
	task task2 weight: 2 { 
		write string(cycle) + ":" + name + "->" + "task2";
	}
}
```

As the **weighted\_tasks** control architecture was chosen, at each simulation step, the dummy agents execute only the task with the highest behavior. Thus,  when _cycle modulo 3_ is higher to 2, task1 is executed; when _cycle modulo 3_ is lower than 2, task2 is executed. In case when _cycle modulo 3_ is equal 2 (at cycle 2, 5, ...), the only the first task defined (here task1) is executed.

Here the result obtained with one dummy agent:
```
0:dummy0->task2
1:dummy0->task2
2:dummy0->task1
3:dummy0->task2
4:dummy0->task2
5:dummy0->task1
6:dummy0->task2
```
