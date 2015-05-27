# User Controlled

---


User controlled architecture has been introduced to allow users to take control over an agent during the course of the simulation. It can be invoked using three different keywords: `user_only`, `user_first`, `user_last`.



<br />

---

## Declaration

Using the Task architectures for a species require to use the **control** facet:

```
species user control: user_only {
   ...
}
```


```
species user control: user_first {
   ...
}
```


```
species user control: user_last {
   ...
}
```

If the control chosen is `user_first`, it means that the user controled panel is opened first, and then the agent has a chance to run its "own" behaviors (reflexes, essentially, or "init" in the case of a "user\_init" panel).
If the control chosen is `user_last`, it is the contrary.

<br />

---


## User Panel

This control architecture is a specialization of the [Finite State Machine Architecture](G__FiniteStateMachine.md) where the "behaviors" of agents can be defined by using new constructs called `user_panel` (and one `user_init`), mixed with "states" or "reflexes". This `user_panel` translates, in the interface, in a semi-modal view that awaits the user to choose action buttons, change attributes of the controlled agent, etc.  Each `user_panel`, like a `state` in FSM, can have a `enter` and `exit` sections, but it is only defined in terms of a set of `user_command`s which describe the different action buttons present in the panel.

user\_commands can also accept inputs, in order to create more interesting commands for the user. This uses the `user_input` statement (and not operator), which is basically the same as a temporary variable declaration whose value is asked to the user. Example:

As `user_panel̀` is a specialization of `state`, the modeler has the possibility to describe several panels and choose the one to open depending on some condition, using the same syntax than for finite state machines :
  * either adding `transitions` to the user\_panels,
  * or setting the `state` attribute to a new value, from inside or from another agent.

This ensures a great flexibility for the design of the user interface proposed to the user, as it can be adapted to the different stages of the simulation, etc..

Follows a simple example, where, every 10 steps, and depending on the value of an attribute called « advanced », either the basic or the advanced panel is proposed.
```
species user control:user_only {
   user_panel default initial: true {
      transition to: "Basic Control" when: every (10) and !advanced_user_control;
      transition to: "Advanced Control" when: every(10) and advanced_user_control;
   }
   
   user_panel "Basic Control" {
      user_command "Kill one cell" {
         ask (one_of(cell)){
            do die;
         }
      }
      user_command "Create one cell" {
        create cell ;
      } 
      transition to: default when: true;                    
   }
   user_panel "Advanced Control" {
      user_command "Kill cells" {
        user_input "Number" returns: number type: int <- 10;
        ask (number among list(cell)){
           do die;
        }
      }
      user_command "Create cells" {
        user_input "Number" returns: number type: int <- 10;
        create cell number: number ;
      } 
      transition to: default when: true;        
   }
}
```

The panel marked with the « initial: true » facet will be the one run first when the agent is supposed to run. If none is marked, the first panel (in their definition order) is chosen.
A special panel called user\_init will be invoked only once when initializing the agent if it is defined.
If no panel is described or if all panels are empty (ie. no user\_commands), the control view is never invoked. If the control is said to be "user\_only", the agent will then not run any of its behaviors.

<br />

---

## User Controlled

Finally, each agent provided with this architecture inherits a boolean attribute called `user_controlled`. If this attribute becomes false, no panels will be displayed and the agent will run "normally" unless its species is defined with a `user_only` control.