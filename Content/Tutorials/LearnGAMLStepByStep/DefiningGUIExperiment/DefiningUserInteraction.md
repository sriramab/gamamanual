# Defining user interaction

During the simulation, GAML provides you the possibility to define some function the user can execute during the execution. In this chapter, we will see how to define buttons to execute action during the simulation, how to catch click event, and how to use the user control architecture.

## Index

* [Catch Mouse Event](#catch-mouse-event)
* [Define User command](#define-user-command)
* [User control architecture](#user-control-architecture)

## Catch Mouse Event

[TODO quand corrig�]

## Define User command

Anywhere in the global block, in a species or in an (GUI) experiment, `user_command` statements can be implemented. They can either call directly an existing action (with or without arguments) or be followed by a block that describes what to do when this command is run.

Their syntax can be (depending of the modeler needs) either:

```
user_command cmd_name action: action_without_arg_name;
//or
user_command cmd_name action: action_name with: [arg1::val1, arg2::val2];
//or
user_command cmd_name {
   // statements
}
```

For instance:

```
user_command kill_myself action: die;
//or
user_command kill_myself action: some_action with: [arg1::5, arg2::3];
//or
user_command kill_myself {
    do die;
}
```

These commands (which belong to the "top-level" statements like actions, reflexes, etc.) are not executed when an agent runs. Instead, they are collected and used as follows:

* When defined in a GUI experiment, they appear as buttons above the parameters of the simulation;
(TODO_IMAGE)
* When defined in the global block or in any species,
**	when the agent is inspected, they appear as buttons above the agents' attributes
(TODO_IMAGE)
**	when the agent is selected by a right-click in a display, these command appear under the usual "Inspect", "Focus" and "Highlight" commands in the pop-up menu. 
(TODO_IMAGE)


Remark: The execution of a command obeys the following rules:
* when the command is called from right-click pop-menu, it is executed immediately
* when the command is called from panels, its execution is postponed until the end of the current step and then executed at that time.

### user_location

In the special case when the `user_command` is called from the pop-up menu (from a right-click on an agent in a display), the location chosen by the user (translated into the model coordinates) is passed to the execution scope under the name `user_location`.

Example:

```
global {
   user_command "Create agents here" {
      create my_species number: 10 with: [location::user_location];
   }
}
```

This will allow the user to click on a display, choose the world (always present now), and select the menu item "Create agents here".

Note that if the world is inspected (this `user_command` appears thus as a button) and the user chooses to push the button, the agent will be created at a random location.

### user_input

As it is also, sometimes, necessary to ask the user for some values (not defined as parameters), the `user_input` unary operator has been introduced. This operator takes a map [string::value] as argument, displays a dialog asking the user for these values, and returns the same map with the modified values (if any). The dialog is modal and will interrupt the execution of the simulation until the user has either dismissed or accepted it. It can be used, for instance, in an init section like the following one to force the user to input new values instead of relying on the initial values of parameters:

```
global {
   init {
      map values <- user_input(["Number" :: 100]);
      create my_species number : int(values at "Number");
   }
}
```

## User control architecture

[TODO quand corrig�]