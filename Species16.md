
<br />
# <font color='blue'>Introduction</font>

A model can contain any number of species. Species are used to specify the structure and behaviors of agents. Although the definitions below apply to all the species, some of them require specific declarations: the species of the world and the species of grids.

# <font color='blue'>Species declaration</font>

The simplest way to declare a species is the following:

```
species a_name {
   [attribute declarations]
   [init]
   [action declarations]
   [behaviors]
   [aspects]
}
```

for example:

```
species foo{} //it is also possible to directly write: species foo;
```

The agents that will belong to this species will only be provided with some [built-in attributes](BuiltInVariables16.md) and actions, a basic behavioral structure and nothing more. So, for instance, it is possible (somewhere else in the model) to write something like:

```
list<foo> foo_agents <- [];
create foo number: 10 return: foo_agents;
ask foo_agents {
   write  "my name is: " + name;
}
```

Which will result in the 10 agents writing their name, in turn, on the console. If the species declare [attributes](Variables16.md), the structure of the agents is modified consequently. For instance:

```
species foo {
    float energy <- rnd (100) min: 0 max: 100 update: energy - 0.001;
}
```

Will give each agent an amount of energy (between 0 and 100), which will decrease over time until it reaches 0.

The species can also declare a statement called _init_ that consists in a set of statements that are executed at the creation of the agents. Here, we provide an init for agents of species foo that will write in the console a specific message.

```
species foo {
    float energy <- rnd (100) min: 0 max: 100 update: energy - 0.001;
    init {
         write "creation of " + name;
    }
}
```

The species can also declare actions that supplement the built-in ones and extend the possibilities of the agents. Here, we provide two possible actions for agents of species foo, eating and stealing energy:

```
species foo {
    float energy <- rnd (100) min: 0 max: 100 update: energy - 0.001;
     init {
         write "creation of " + name;
    }
    action eat {
        energy <- energy + rnd (2);
    }
    action steal {
        foo another_agent <- any (foo  - self);
        if (another_agent != nil) and ((another_agent.energy) > 0){
           another_agent.energy <- another_agent.energy - 0.01;
           energy <- energy + 0.01;
        }
    }
}
```

Of course, these actions do nothing unless they are called either by behaviors or by other agents. One might for example extend the previous example like:

```
list<foo> foo_agents <- [];
create foo number: 1000 return: foo_agents;
ask (100 among (foo)) {
    do eat;
}
ask (100 among (foo)) {
    do steal;
}
```

In this example, we create 1000 foos, ask 100 of them to eat, and another 100 of them to steal energy. If these commands are done repetitively (for example, every step), they will result in a somewhat complex dynamic distribution of the energy between the foos.

Of course, the dynamics of foos can also be declared from within their species. If we change slightly the declaration of foo like this:

```
species foo {
    float energy <- rnd (100) min: 0 max: 100 update: energy - 0.001;
     init {
         write "creation of " + name;
    }
    action eat {
        energy <- energy + rnd (2);
    }
    action steal {
        foo another_agent <- any (foo - self);
        if (another_agent != nil) and ((another_agent.energy) > 0){
           another_agent.energy <- another_agent.energy - 0.01;
           energy <- energy + 0.01;
        }
   }
   reflex {
        if flip (0.1) {
           do eat;
        }
        if  flip (0.1) {
           do steal;
        }
    }
}
```

We obtain agents that execute the reflex every turn and decide independently to eat or steal energy. Once they are created using

```
create foo number:1000;
```

they behave on their own.


# <font color='blue'>Skills: behavioral plug-ins</font>

Basic agents like the previous ones cannot, however, do many things. That's what skills are for. Example:

```
species foo skills: [moving]{
  ...
}
```

makes foos benefit from a set of attributes and actions declared by the _moving_ skill. Skills are like plug-ins written in Java and can provide a lot of new functionalities to the agents.

More details about skills are available [here](Skills16.md).

# <font color='blue'>Parent: inheritance of species</font>

A species can be declared as a child of another species, using the parent property. For instance :

```
species foo skills:[moving] parent:bar {
  ...
}
```

will make foo "inherit" from the definition of bar. What does "inherit" precisely mean in this context ?

  * skills declared in bar, together with their built-in attributes and actions, are copied to foo and added to the possible new skills defined in foo.
  * attributes declared in bar, are identically copied to foo unless an attribute with the same name is defined in foo, in which case this redefinition is kept. This also applies to built-in attributes. The type of the attribute can be changed in this process as well (but be careful when doing it, since inherited behaviors can rely on the previous type).
  * actions declared in bar are identically copied to foo unless an action with the same name is defined in foo, in which case this redefinition is kept.
  * reflexes declared in bar are identically copied to foo unless a reflex with the same name is defined in foo, in which case this redefinition is kept. Unnamed reflexes from both species are kept in the definition of foo.
  * behaviors declared in bar are identically copied to foo unless a behavior of the same type with the same name is defined in foo, in which case this redefinition is kept.
  * inits are treated differently : each of the init statement defined in bar and foo are kept in foo and they are executed in the order of inheritance (ie. bar 's one first, then foo 's one).

# <font color='blue'>Scheduling description</font>
The modeler can specify the scheduling information of a species. This scheduling information is composed of the execution frequency and the list of agent to be scheduled.

  * the execution frequency is the frequency which agents of the species are considered to be scheduled.
  * "the list of agent to be scheduled" is an expression returning a list of agent dynamically evaluated at runtime.

```
species foo skills:[moving] parent:bar frequency: 2 schedules: foo where (each.energy > 50)  {
    float energy <- rnd (100) min: 0 max: 100 value: energy - 0.001;
  ...
}
```

  * frequency: we schedule the agents declared in `schedules:` every 2 simulation steps (or all the agents if `schedules:` is not defined).
  * schedules: an expression that returns the list of agent to be scheduled, in that case all the foo agents having a level of energy greater than 50.

# <font color='blue'>Topology description</font>
The topology describes the spatial organization of the species. This imposes constraint on the movement and perception (neighborhood) of the species' agents. GAMA supports three types of topology: continuous, grid and graph.

![http://gama-platform.googlecode.com/files/topologies.png](http://gama-platform.googlecode.com/files/topologies.png)

```
species foo skills:[moving] parent:bar topology: (square (10)) at_location {50, 50}  {
  ...
}
```

Topology of the "foo" species is a square of 10 meters each side at location {50, 50}.


Note that it is possible to declare species of agents with a grid topology using the grid definition (see [here](Grid16.md)).

# <font color='blue'>Nesting species</font>
A species can be defined inside another species. The enclosing species becomes its macro-species. The enclosed species are its micro-species. The "global" species is the top-level species of a model (actually, it represents the model itself). The possibility to establish micro-macro relationships, to specify the [scheduling description](#Scheduling_description.md) and the [topology description](#Topology_description.md) enable the modeler to develop multi-scale models quite easily.

```
species A  {
  ...
}

species B {
   species C parent: A {
   ...
   }

   species D {
   ...
   }
}
```

  * "A" and "B" are micro-species of the "global" species.
  * "C" and "D" are micro-species of the "B" species.
  * "C" species is a sub-species of "A". So agents of "A" can be [captured](Commands14#capture.md) by an agent of "B" species to become a "C" agent, micro-agent of the "B" agent. Vice-versa, a "C" agent, micro-agent of a "C" agent, can be [released](Commands14#release.md) from the "C" agent to become an "A" agent.

# <font color='blue'>"control:" facet. Defining the behavioral architecture</font>

By default, species are created with a minimal behavioral architecture : they only allow the definition of reflexes as a way to define the agents' behaviors. As reflex-based agents are somewhat limited when it comes to maintaining a state between two steps or enabling the selection of behaviors, GAML provides the modeler with several possible behavioral architectures, for example FSM (Finite State Machines). or task-based architecture Each of them gives the possibility to define new elements in addition to reflexes : respectively tasks and states, which can maintain a persistent state over the steps. See [here](Behaviors16.md) for more information. In addition, the behaviors of agents can be completely or partially taken in charge by the user, with a choice of [user control architectures](UserControl16#user_control_architecture.md).

# <font color='blue'>Base: Java foundation</font>

The corresponding class used to initialize agent. An advance feature of the GAMA platform allowing the third party developer to develop their own agent architecture using the Java programming language.