# Multi-level Architecture (Under Construction)
<font color='red'><i>todo</i>:<br>
<ul><li>Explain a little bit more what the meaning of the "multi-level" architecture is.<br>
</li><li>Link to the general architecture of GAMA (the "world" agent being the "host" of regular agents, etc.)<br>
</li><li>Perhaps choose a simple example (with no "birds", etc.) but only micro_agent and macro_agent<br>
</li><li>explains what it means in terms of scheduling and topology<br>
</font>
<hr />
The multi-level architecture offers the modeller the following possibilities : (1) the declaration of a species as a micro-species of another species, (2) the representation of an entity as different types of agent (i.e., GAML species), (3) the dynamic migration of agents between populations.</li></ul>



# Details
## Declaration of micro-species
A species can have other species as micro-species. The micro-species of a species is declared inside the species' declaration.

```
   species group {
      ...
 
      species bird_in_group {
      ...
      }

      ...
   }
```

In the above example, "bird\_in\_group" is a micro-species of "group" species. An agent of "group" species can have agents "bird\_in\_group" species as micro-agents. Agents of "bird\_in\_group" species have an agent of "group" species as "host" agent.

## Representation of an entity as different types of agent
Let's imagine two scenarios of a "bird" entity. Firstly, when a "bird" entity flies alone the modeler would like to represent it in one way (e.g., with a lot of detail). Secondly, when a "bird" entities flies in group (a group of birds is in fact a set of nearby flying bird), the modeler would like to represent it in another way (e.g., less detail and introduce some constraints between nearby birds). In GAML, the modeler can program this as follows:

```

   species bird {
   ...
   }

   species group {
      ...
 
      species bird_in_group parent: bird {
      ...
      }

      ...
   }
```

The "bird" entity is represented as two species: "bird" and "bird\_in\_group". The special point to remember here is that "bird\_in\_group" must be a sub-species of "bird" species.

## Dynamic migration of agents
In our example, a "group" entity is composed of nearby flying "bird" entities. When a "bird" entity approaches a "group" entity, this "bird" entity will become a member of the group. To represent this, the modeler lets the "bird" agent change its species to "bird\_in\_group" species. The "bird" agent hence becomes a "bird\_in\_group" agent. To change species of agent, we can use one of the following statements : [capture](G__Statements), [release](G__Statements), [migrate](G__Statements).

For example, in this case, to model the fact that a "group" agent captures the nearby "bird" agents (within a 5 meters distance from the group) as "bird\_in\_group" agents. We can write something as follows:

```

   species bird {
   ...
   }

   species group {
      ...
 
      species bird_in_group parent: bird {
      ...
      }

      reflex capture_nearby_free_birds {
	  list<bird> nearby_birds <- (bird overlapping (shape + 5));
	  if !(empty (nearby_birds)) {
	    capture nearby_birds as: bird_in_group;
	  }
      }

      ...
   }
```




## Access to micro-agents, host agent
An agent can access to its micro-agents and host thanks to two built-in variables : "members" and "host".

For example, a "group" agent can access to its micro-agents of "bird\_in\_group" species as follows :

```
   species group {
      ...
 
      species bird_in_group parent: bird {
      ...
      }

      species other_micro_species {
      ...
      }

      reflex print {
        let<bird_in_group> my_bird_members <- members of_species bird_in_group;
        write my_bird_members;
      }

      ...
   }
```

A "bird\_in\_group" agent can access to its host as follows:
```
   species group {
      ...
 
      species bird_in_group parent: bird {
         reflex print_host {
           write 'my host agent is ' + host;
         }
      }

      ...
   }
```