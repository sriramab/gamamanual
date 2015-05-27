# Built-in Control Architectures

---

GAMA allows to attach built-in control architecture to agents.

These control architectures will give the possibility to the modeler to use for a species a specific control architecture in addition to the [common behavior structure](G__DefiningBehaviors.md). Note that only one control architecture can be used per species.


<br />

---

## Attachment of Control Architecture
The attachment of a control architecture to a species is done through the facets **control**.

For example, the given code allows to attach the _fsm_ control architecture to the dummy species.
```
species dummy control: fsm {
}
```

<br />

---

## List of Control Architectures
GAMA integrates several agent control architectures that can be used in addition to the common behavior structure:
  * [fsm](G__FiniteStateMachine.md): finite state machine based behavior model. During its life cycle, the agent can be in several states. At any given time step, it is in one single state. Such an agent needs to have one initial state (the state in which it will be at its initialization)
  * [weighted\_tasks](G__TaskBased.md): task-based control architecture. At any given time, only the task only the task with the maximal weight is executed.
  * [sorted\_tasks](G__TaskBased.md): task-based control architecture. At any given time, the tasks are all executed in the order specified by their weights (highest first).
  * [probabilistic\_tasks](G__TaskBased.md): task-based control architecture. This architecture uses the weights as a support for making a weighted probabilistic choice among the different tasks. If all tasks have the same weight, one is randomly chosen at each step.
  * [user\_only](G__UserControlled.md): allows users to take control over an agent during the course of the simulation. With this architecture, only the user control the agents (no reflexes).
  * [user\_first](G__UserControlled.md): allows users to take control over an agent during the course of the simulation. With this architecture, the user actions are executed before the agent reflexes.
  * [user\_last](G__UserControlled.md): allows users to take control over an agent during the course of the simulation. With this architecture, the user actions are executed after the agent reflexes.