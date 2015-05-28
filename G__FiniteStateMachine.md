# Finite State Machine




FSM (Finite State Machine) is a finite state machine based behavior model. During its life cycle, the agent can be in several states. At any given time step, it is in one single state. Such an agent needs to have one initial state (the state in which it will be at its initialization).

At each time step, the agent will:
  * first (only if he just entered in its current state) execute statement embedded in the `enter` statement,
  * then all the statements in the state statement
  * it will evaluate the condition of each embedded transition statements. If one condition is fulfilled, the agent execute the embedded statements

Note that an agent executes only one state at each step.







## Declaration


Using the FSM architecture for a species require to use the **control** facet:

```
species dummy control: fsm {
   ...
}
```







## State

### Attributes
  * initial: a boolean expression, indicates the initial state of agent.
  * final: a boolean expression, indicates the final state of agent.

### Sub Statements
  * enter: a sequence of statements to execute upon entering the state.
  * exit: a sequence of statements to execute right before exiting the state. Note that the `exit` statement will be executed even if the fired transition points to the same state (the FSM architecture in GAMA does not implement 'internal transitions' like the ones found in UML state charts: all transitions, even "self-transitions", follow the same rules).
  * transition: allows to define a condition that, when evaluated to true, will designate the next state of the life cycle. Note that the evaluation of transitions is short-circuited: the first one that evaluates to true, in the order in which they have been defined, will be followed. I.e., if two transitions evaluate to true during the same time step, only the first one will be triggered.

Things worth to be mentioned regarding these sub-statements:
  * Obviously, only one definition of exit and enter is accepted in a given state
  * Transition statements written in the middle of the state statements will only be evaluated at the end, so, even if it evaluates to true, the remaining of the statements found after the definition of the transition will be nevertheless executed. So, despite the appearance, a transition written somewhere in the sequence will "not stop" the state at that point (but only at the end).

### Definition
A state can contain several statements that will be executed, at each time step, by the agent. There are three exceptions to this rule:
  1. statements enclosed in `enter` will only be executed when the state is entered (after a transition, or because it is the initial state).
  1. Those enclosed in `exit` will be executed when leaving the state as a result of a successful transition (and before the statements enclosed in the transition).
  1. Those enclosed in a transition will be executed when performing this transition (but after the `exit` sequence has been executed).

For example, consider the following example:
```
species dummy control: fsm {       
	state state1 initial: true { 
		write string(cycle) + ":" + name + "->" + "state1";
		transition to: state2 when: flip(0.5) {
			write string(cycle) + ":" + name + "->" + "transition to state1";
		}
		transition to: state3 when: flip(0.2) ; 
	}

	state state2 {
		write string(cycle) + ":" + name + "->" + "state2";
		transition to: state1 when: flip(0.5) { 
			write string(cycle) + ":" + name + "->" + "transition to state1";
		}
		exit {
			write string(cycle) + ":" + name + "->" + "leave state2";
		}
	}
	
	state state3 {
		write string(cycle) + ":" + name + "->" + "state3";
		transition to: state1 when: flip(0.5)  {
			write string(cycle) + ":" + name + "->" + "transition to state1";
		}
		transition to: state2 when: flip(0.2)  ;
	}   
}
```

the dummy agents start at _state1_. At each simulation step they have a probability of 0.5 to change their state to _state2_. If they do not change their state to _state2_, they have a probability of 0.2 to change their state to _state3_. In _state2_, at each simulation step, they have a probability of 0.5 to change their state to _state1_. At last, in _step3_, at each simulation step they have a probability of 0.5 to change their state to _state1_. If they do not change their state to _state1_, they have a probability of 0.2 to change their state to _state2_.

Here a possible result that can be obtained with one dummy agent:
```
0:dummy0->state1
0:dummy0->transition to state1
1:dummy0->state2
2:dummy0->state2
2:dummy0->leave state2
2:dummy0->transition to state1
3:dummy0->state1
3:dummy0->transition to state1
4:dummy0->state2
5:dummy0->state2
5:dummy0->leave state2
5:dummy0->transition to state1
6:dummy0->state1
7:dummy0->state3
8:dummy0->state2
```