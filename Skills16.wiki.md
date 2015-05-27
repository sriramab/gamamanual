
<br />
# <font color='blue'>Overview</font>

Skills are built-in modules that provide a set of related built-in variables and built-in actions (in addition to those already provided by GAMA) to the species that declare them. A declaration of skill is done by filling the skills attribute in the species definition:

```
species my_species skills: [skill1, skill2] {
    ...
}
```

Skills have been designed to be mutually compatible so that any combination of them will result in a functional species. The list of available skills in GAMA is:
  * moving: for agents that need to move.

So, for instance, if a species is declared as:

```
species foo skills: [moving]{
...
}
```

its agents will automatically be provided with the following variables : "speed, heading, destination (r/o)" and the following actions: "move, goto, wander, follow" in addition to those built-in in species and declared by the modeller. Most of these variables, except the ones marked read-only, can be customized and modified like normal variables by the modeller. For instance, one could want to set a maximum for the speed; this would be done by redeclaring it like this:

```
float speed max:100 min:0;
```

Or, to obtain a speed increasing at each simulation step:

```
float speed max:100 min:0  <- 1 update: speed * 1.01;
```

Or, to change the speed in a behavior:

```
if speed = 5 {
    speed <- 10;
}
```


# <font color='blue'>moving</font>

## variables
### speed
  * float, the speed of the agent, in meter/second.

### heading
  * int, the absolute heading of the agent in degrees (in the range 0-359).

### destination
  * point, read-only, continuously updated destination of the agent with respect to its speed and heading.

## actions

### follow
moves the agent along a given path passed in the arguments.
  * → **speed**: float, optional, the speed to use for this move (replaces the current value of speed).
  * → **path**: a path to be followed

```
do follow speed: speed * 2 path: road_path;
```

### goto
moves the agent towards the target passed in the arguments.
  * → **target**: point or agent, mandatory, the location or entity towards which to move.
  * → **speed**: float, optional, the speed to use for this move (replaces the current value of speed).
  * → **on**: list, agent, graph, geometry, optional, that restrains this move (the agent moves inside this geometry).
  * → **return\_path** : bool, optional, if true, the action returns the path followed
  * ← return: null or the path followed if **return\_path**  is set to _true_

```
do goto target: one_of (list (species (self))) speed: speed * 2 on: road_network;
```

### move
moves the agent forward, the distance being computed with respect to its speed and heading. The value of the corresponding variables are used unless arguments are passed.
  * → **speed**: float, optional, the speed to use for this move (replaces the current value of speed).
  * → **heading**: int, optional, the direction to take for this move (replaces the current value of heading).
  * → **bounds**: localized entity, optional, the geometry (the localized entity geometry) that restrains this move (the agent moves inside this geometry).

```
do move speed: speed - 10 heading: heading + rnd (30) bounds: agentA;
```

### wander
moves the agent towards a random location at the maximum distance (with respect to its speed). The heading of the agent is chosen randomly if no amplitude is specified. This action changes the value of heading.
  * → **speed**: float, optional, the speed to use for this move (replaces the current value of speed).
  * → **amplitude**: int, optional, a restriction placed on the random heading choice. The new heading is chosen in the range (heading - amplitude/2, heading+amplitude/2).
  * → **bounds**: localized entity or geometry, optional, the geometry (the localized entity geometry) that restrains this move (the agent moves inside this geometry).

```
do wander speed: speed - 10 amplitude: 120 bounds: agentA;
```


# <font color='blue'>communicating</font>
The communicating skill offers some primitives and built-in variables which enable agent to communicate using the FIPA interaction protocol.

## variables
Agents with such a skill will automatically be provided with the following built-in variables : "conversations, messages, accept\_proposals, agrees, cancels, cfps, failures, informs, proposes, queries, refuses, reject\_proposals, requests, requestWhens, subscribes". They will also be provided with the following actions: "send, reply, accept\_proposal, agree, cancel, cfp, end, failure, inform, propose, query, refuse, reject, request, subcribe".

### message
  * **Definition:** A GAML type that represents the FIPA ACL message.

  * **Built-in attributes:**
    * sender, agent, the sender of the message.
    * receivers, list of agent, the receivers of the message.
    * performative, string, the performative of the message.
    * content, list, the content of the message.
    * unread, bool, true if the message has not yet been read and false otherwise. A message is considered as already read if its "content" field is accessed. An already read message will be automatically removed from the mailbox of agent, the modeler thus doesn't have to manually removed the already read messages.
    * conversation, conversation, the conversation that the message belongs to.
    * protocol, string, the interaction protocol of the conversation.
    * timestamp, string, the creation time of the message.



### conversation
  * **Definition:** A GAML type that represents the FIPA ACL interaction protocol. We support 8 standard FIPA interaction protocols (fipa-brokering, fipa-contract-net, fipa-interated-contract-net, fipa-propose, fipa-query, fipa-request, fipa-request-when, fipa-subscribe). When a conversation follows a (supported) FIPA interaction protocol, the series of exchanged messages (i.e., their performatives) have to respect the corresponding FIPA specification otherwise a GAMA runtime exception will be thrown on the GAMA graphical user interface. We support a special interaction protocol: "no-protocol". With a "no-protocol" conversation, the modeler is free to send messages with any performative type. To mark the end of a "no-protocol" conversation, an agent sends a message having "end" as performative. A conversation is removed from the "conversations" list of agent if it is ended and all of its messages have already been read.

  * **Built-in attributes:**
    * messages, list of messages, all the messages of this conversation.
    * protocol, string, the interaction protocol of the conversation.
    * initiator, agent, the initiator of the conversation.
    * participants, list of agents, the participant(s) of the conversation.
    * ended, bool, true of the conversation has already ended and false otherwise.


### built-in variables
  * conversations, list, the current conversations of the agent.
  * messages, list, all the messages in the mailbox of agent.
  * accept\_proposals, list, all the messages in the mailbox having "accept-proposal" performative.
  * agrees, list, all the messages in the mailbox having "agree" performative.
  * cancels, list, all the messages in the mailbox having "cancel" performative.
  * cfps,list, all the messages in the mailbox having "cfp" (call for proposal) performative.
  * failures, list, all the messages in the mailbox having "failure" performative.
  * informs, list, all the messages in the mailbox having "inform" performative.
  * proposes, list, all the messages in the mailbox having "propose" performative.
  * queries, list, all the messages in the mailbox having "query" performative.
  * refuses, list, all the messages in the mailbox having "refuse" performative.
  * reject\_proposals, list, all the messages in the mailbox having "reject\_proposal" performative.
  * requests, list, all the messages in the mailbox having "request" performative.
  * requestWhens, list, all the messages in the mailbox having "request\_when" performative.
  * subscribes, list, all the messages in the mailbox having "subscribe" performative.


## actions

### send
sends a message to other(s) agent(s). This message is used to begin a conversation.
  * → **receivers**: list of agent, mandatory, the receivers of the message.
  * → **protocol**: string, mandatory, the name of a protocol.
  * → **performative**: string, mandatory, the name of a performative.
  * → **content**: list of object, optional, the content of the message.


### reply
replies a message.
  * → **message**: message, mandatory, the receiving message that we would like to reply.
  * → **performative**: string, mandatory, the performative of the replying message.
  * → **content**: list of object, optional, the content of the replying message.

### accept\_proposal
replies a message with "accept\_proposal" performative.
  * → **message**: message, mandatory, the receiving message that we would like to reply.
  * → **content**: list of object, optional, the content of the replying message.

### agree
replies a message with "agree" performative.
  * → **message**: message, mandatory, the receiving message that we would like to reply.
  * → **content**: list of object, optional, the content of the replying message.

### cancel
replies a message with "cancel" performative.
  * → **message**: message, mandatory, the receiving message that we would like to reply.
  * → **content**: list of object, optional, the content of the replying message.

### cfp
replies a message with "cfp" performative.
  * → **message**: message, mandatory, the receiving message that we would like to reply.
  * → **content**: list of object, optional, the content of the replying message.

### end
replies a message with "end" performative.
  * → **message**: message, mandatory, the receiving message that we would like to reply.
  * → **content**: list of object, optional, the content of the replying message.

### failure
replies a message with "failure" performative.
  * → **message**: message, mandatory, the receiving message that we would like to reply.
  * → **content**: list of object, optional, the content of the replying message.

### inform
replies a message with "inform performative.
  * → **message**: message, mandatory, the receiving message that we would like to reply.
  * → **content**: list of object, optional, the content of the replying message.

### propose
replies a message with "propose" performative.
  * → **message**: message, mandatory, the receiving message that we would like to reply.
  * → **content**: list of object, optional, the content of the replying message.

### query
replies a message with "query" performative.
  * → **message**: message, mandatory, the receiving message that we would like to reply.
  * → **content**: list of object, optional, the content of the replying message.

### refuse
replies a message with "refuse" performative.
  * → **message**: message, mandatory, the receiving message that we would like to reply.
  * → **content**: list of object, optional, the content of the replying message.

### reject\_proposal
replies a message with "reject\_proposal" performative.
  * → **message**: message, mandatory, the receiving message that we would like to reply.
  * → **content**: list of object, optional, the content of the replying message.

### request
replies a message with "request" performative.
  * → **message**: message, mandatory, the receiving message that we would like to reply.
  * → **content**: list of object, optional, the content of the replying message.

### subscribe
reply a message with "subscribe" performative.
  * → **message**: message, mandatory, the receiving message that we would like to reply.
  * → **content**: list of object, optional, the content of the replying message.

## Sample models
Please find some toy sample models in the "fipa" folder bundle with the GAMA's model library.


This extensions of GAMA is a new skill that extends the moving skill and that provides new moving actions that take into account the traffic jam and the number of lanes of roads. This skill is implemented in the simtools.gaml.extensions.traffic plug-in.


# <font color='blue'>driving</font>
Agents with such a skill will automatically be provided with the variables of the [moving](Skills16#moving.md) skill ("speed, heading, destination (r/o)") and the following variables : "living\_space, lanes\_attribute, tolerance, obstacle\_species". They will also be provided with the action of the [moving](Skills16#moving.md) skill ("move, goto, wander, follow") and the following action: "moveTraffic".

## variables
### living\_space
  * float, the min distance between the agent and an obstacle (in meter).

### lanes\_attribute
  * string, the name of the attribut of the road agent that determine the number of road lanes.

### tolerance
  * float, the tolerance distance used for the computation (in meter).

### obstacle\_species
  * list of species, the list of species that are considered as obstacles.

## actions

### follow\_driving
moves the agent along a given path passed in the arguments. . When moving on a road section, an agent cannot pass through **n** obstacles excepts if the number of lanes for this road section is equal or higher than **n+1**.
  * → **speed**: float, optional, the speed to use for this move (replaces the current value of speed).
  * → **path**: a path to be followed
  * → **living\_space** : float, optional, min distance between the agent and an obstacle (replaces the current value of living\_space).
  * → **tolerance** : float, optional, tolerance distance used for the computation (replaces the current value of tolerance).
  * → **lanes\_attribute** : string, optional, the name of the attribut of the road agent that determine the number of road lanes (replaces the current value of lanes\_attribute)

```
do follow_driving path: road_path speed: speed living_space: 2.0;
```

### goto\_driving
moves the agent towards the target passed in the arguments. When moving on a road section, an agent cannot pass through **n** obstacles excepts if the number of lanes for this road section is equal or higher than **n+1**.
  * → **target**: point or agent, mandatory, the location or entity towards which to move.
  * → **speed**: float, optional, the speed to use for this move (replaces the current value of speed).
  * → **on**: list, agent, graph, geometry, optional, that restrains this move (the agent moves inside this geometry).
  * → **return\_path** : bool, optional, if true, the action returns the path followed.
  * → **living\_space** : float, optional, min distance between the agent and an obstacle (replaces the current value of living\_space).
  * → **tolerance** : float, optional, tolerance distance used for the computation (replaces the current value of tolerance).
  * → **lanes\_attribute** : string, optional, the name of the attribut of the road agent that determine the number of road lanes (replaces the current value of lanes\_attribute)
  * → **return\_path** : bool, optional, if true, the action returns the path followed
  * ← return: null or the path followed if **return\_path**  is set to _true_

```
do goto_driving target: the_target on: road_network speed: speed living_space: 2.0;
```

## Sample models
Three models based on this plug-in are available in GAMA 1.5.1: `RoadTrafficSimple`, `RoadTrafficComplex` and `RoadTrafficCity`. These models are defined in the driving\_traffic project.

  * `RoadTrafficSimple`
![http://gama-platform.googlecode.com/files/modelSimple.png](http://gama-platform.googlecode.com/files/modelSimple.png)

  * `RoadTrafficCity`
![http://gama-platform.googlecode.com/files/ModelCity.png](http://gama-platform.googlecode.com/files/ModelCity.png)