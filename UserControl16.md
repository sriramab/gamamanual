

# <font color='blue'> Introduction </font>

GAMA provides some tools to give more flexibility to the user in controlling the agents, creating agents, killing agents, running specific actions, etc.

# <font color='blue'> user_command </font>

Anywhere in the global block, in a species or in an (GUI) experiment, `user_command` statements can be implemented. They can either call directly an existing action (with or without arguments) or be followed by a block that describes what to do when this command is run.

Their syntax can be (depending of the modeler needs) either:
```
user_command cmd_name action: action_without_arg_name;
```
or
```
user_command cmd_name action: action_name with: [arg1::val1, arg2::val2, ...];
```
or
```
user_command cmd_name {
   [statements]
}
```


For instance :
```
user_command kill_myself action: die;
```
or
```
user_command kill_myself action: some_action with: [arg1::val1, arg2::val2, ...];
```
or
```
user_command kill_myself {
    do action: die;
}
```


These commands (which belong to the "top-level" statements like actions, reflexes, etc.) are not executed when an agent runs. Instead, they are collected and used as follows:
  * When defined in a GUI experiment, they appear as buttons above the parameters of the simulation;
  * When defined in the global block or in any species,
    * when the agent is inspected, they appear as buttons above the agents' attributes
    * when the agent is selected by a right-click in a display, these command appear under the usual "Inspect", "Focus" and "Highlight" commands in the pop-up menu.

Remark: The execution of a command obeys the following rules:
  * when the command is called from right-click pop-menu, it is executed immediately,
  * when the command is called from panels, its execution is postponed until the end of the current step and then executed at that time.


# <font color='blue'> user_location </font>

In the special case when the user\_command is called from the pop-up menu (from a right-click on an agent in a display), the location chosen by the user (translated into the model coordinates) is passed to the execution scope under the name **`user_location`**.

Example :
```
global {
   user_command "Create agents here" {
      create my_species number: 10 with: [location::user_location];
   }
}
```

This will allow the user to click on a display, choose the world (always present now), and select the menu item "Create agents here".

Note that if the world is inspected (this user\_command appears thus as a button) and the user chooses to push the button, the agent will be created at a random location.


# <font color='blue'> <code>user_input</code> operator </font>

As it is also, sometimes, necessary to ask the user for some values (not defined as parameters), the user\_input unary operator has been introduced. This operator takes a map [string::value] as argument, displays a dialog asking the user for these values, and returns the same map with the modified values (if any). The dialog is modal and will interrupt the execution of the simulation until the user has either dismissed or accepted it. It can be used, for instance, in an init section like the following one to force the user to input new values instead of relying on the initial values of parameters :
```
global {
   init {
      let values type: map <- user_input(["Number" :: 100, "Location" :: {10, 10}]);
      create my_species number : int(values at "Number") with: [location:: (point(values at "Location"))];
   }
}
```


# <font color='blue'>user control architecture </font>

## user\_only, user\_first, user\_last

A new type of control architecture has been introduced to allow users to take control over an agent during the course of the simulation. It can be invoked using three different keywords: `user_only`, `user_first`, `user_last`.
```
species user control: user_only {
   ...
}
```

If the control chosen is `user_first`, it means that the user controled panel is opened first, and then the agent has a chance to run its "own" behaviors (reflexes, essentially, or "init" in the case of a "user\_init" panel).
If the control chosen is `user_last`, it is the contrary.


## user\_panel

This control architecture is a specialization of the Finite State Machine Architecture where the "behaviors" of agents can be defined by using new constructs called `user_panel` (and one `user_init`), mixed with "states" or "reflexes". This `user_panel` translates, in the interface, in a semi-modal view that awaits the user to choose action buttons, change attributes of the controlled agent, etc.  Each `user_panel`, like a `state` in FSM, can have a `enter` and `exit` sections, but it is only defined in terms of a set of `user_command`s which describe the different action buttons present in the panel.

Example, in the circle.gaml model :
```
species user control:user_only {
		
   user_panel "Basic Control"{
      user_command "Kill one cell" {
	 ask (one_of(cells)){
	    do die;
	 }
      }
      user_command "Create one cell" {
	create cells number: 1;
      }			
   }
}
```

this will create a simple panel like the one on the following image.

http://gama-platform.googlecode.com/files/BasicPanel.PNG


user\_commands can also accept inputs, in order to create more interesting commands for the user. This uses the `user_input` statement (and not operator), which is basically the same as a temporary variable declaration whose value is asked to the user. Example:
```
user_command "Kill cells" {
   user_input "Number" returns: number type: int <- 10;
   ask (number among list(cells)){
	do die;
   }
}
```

It translates into a button + an input (as depicted on the following image).

http://gama-platform.googlecode.com/files/AdvancedPanel.PNG

Several inputs are of course allowed (see « Create Cells » on the same panel).
```
   user_command "Create cells" {
      user_input "Number" returns: number type: int <- 10;
      user_input "Location" returns: loc type: point <- {0,0};
      create cells number: number with: [location::loc];
   } 
```

As `user_panel̀` is a specialization of `state`, the modeler has the possibility to describe several panels and choose the one to open depending on some condition, using the same syntax than for finite state machines :
  * either adding `transitions` to the user\_panels,
  * or setting the `state` attribute to a new value, from inside or from another agent.

This ensures a great flexibility for the design of the user interface proposed to the user, as it can be adapted to the different stages of the simulation, etc..

Follows a simple example, where, every 10 steps, and depending on the value of an attribute called « advanced », either the basic or the advanced panel is proposed.
```
species user control:user_only{		
   bool advanced <- false;

   user_panel default initial: true {
      transition to: "Basic Control" when: every (10) and !advanced;
      transition to: "Advanced Control" when: every(10) and advanced;
   }
		
   user_panel "Advanced Control" {
      user_command "Kill cells" {
	user_input "Number" returns: number type: int <- 10;
	ask (number among list(cells)){
	   do die;
	}
      }
      user_command "Create cells" {
	user_input "Number" returns: number type: int <- 10;
	user_input "Location" returns: loc type: point <- {0,0};
	create cells number: number with: [location::loc];
      } 
      user_command "Kill user" {
	do die;
      }
      transition to: default when: true;	
   }
		
   user_panel "Basic Control"{
      user_command "Kill one cell" {
	ask (one_of(cells)){
	   do die;
	}
      }
      user_command "Create one cell" {
	create cells number: 1;
      }
      transition to: default when: true;			
   }
}
```

The panel marked with the « initial: true » facet will be the one run first when the agent is supposed to run. If none is marked, the first panel (in their definition order) is chosen.
A special panel called user\_init will be invoked only once when initializing the agent if it is defined.
If no panel is described or if all panels are empty (ie. no user\_commands), the control view is never invoked. If the control is said to be "user\_only", the agent will then not run any of its behaviors.


## user\_controlled

Finally, each agent provided with this architecture inherits a boolean attribute called `user_controlled`. If this attribute becomes false, no panels will be displayed and the agent will run "normally" unless its species is defined with a `user_only` control.