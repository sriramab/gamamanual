# 1. Loading of GIS Data
This second step consists in defining the gold miner agents using the GAMA BDI architecture.

## Formulation
  * Definition of global predicates
  * Definition of the gold miner species
  * Definition of the gold miner perceptions
  * Definition of the gold miner rules
  * Definition of the gold miner plans
  * Creation and display of the gold miners


## BDI agents
A classic paradigm to formalize the internal architecture of cognitive agents in Agent-Oriented Software Engineering is the BDI (Belief-Desire-Intention) paradigm. This paradigm, based on the philosophy of action [(Bratman, 1987)](https://philpapers.org/rec/braipa), allows to design expressive and realistic agents. 

The concepts of Belief-Desire-Intention can be summarized as follow for the the Gold Miner: the Miner agent has a general desire to find gold. As it is the only thing it wants at the beginning, it is its initial intention (what it is currently doing). To find gold, it wanders around (its plan is to wander). When it perceives some gold nuggets, it stores this information (it has a new belief about the existence and location of this gold nugget), and it adopts a new desire (it wants to extract the gold). When it perceives a gold nugget, the intention to find gold is put on hold and a new intention is selected (to extract gold). To achieve this intention, the plan has two steps, i.e. two new (sub)intentions: to choose a gold nugget to extract (among its known gold nuggets) and to go and take it. And so on.

We propose in GAMA a control architecture for agents based on this paradigm. This control architecture provides the agents with 3 database linked to the agent cognition:
* **belief_base** (what it knows): the internal knowledge the agent has about the world or about its internal state, updated during the simulation. A belief can concern any type of information (a quantity, a location, a boolean value, etc).
* **desire_base** (what it wants): objectives that the agent would like to accomplish, also updated during the simulation. Desires can have hierarchical links (sub/super desires) when a desire is created as an intermediary objective.
* **intention_base** (what it is doing): what the agent has chosen to do. The current intention will determine the selected plan. Intentions can be put on hold (for example when they require a sub-intention to be achieved).

In addition, the BDI architecture provides agents with three types of behavior structures
* **Perception**: a perception is a function executed at each iteration to update the agent’s Belief base, to know the changes in its environment (the world, the other agents and itself). The agent can perceive other agents up to a fixed distance or inside a specific geometry. 
* **Rule**: a rule is a function executed at each iteration to infer new desires or beliefs from the agent’s current beliefs and desires, i.e. a new desire or belief can emerge from the existing ones. 
* **Plan**: the agent has a set of plans, which are behaviors defined to accomplish specific intentions. Plans can be instantaneous and/or persistent, and may have a priority value (that can be dynamic), used to select a plan when several possible plans are available to accomplish the same intention.

To be more precise on the behavior of BDI agents (what the agent is going to do when activated), this one is composed of 10 steps (see [(Caillou et al., 2017)](https://hal.archives-ouvertes.fr/hal-01216165/document) and [(Taillandier et al., 2016)](https://hal.archives-ouvertes.fr/hal-01391002/document) for more details):
1. _Perceive_: Perceptions are executed.
1. _Rule_: Rules are executed.
1. _Is one of my intentions achieved?_: If one of my intentions is achieved, sets the current plan to nil and removes the intention from the intention base. If the achieved intention’s super-intention is on hold, it is reactivated (its sub-intention just got completed).
1. _Do I keep the current intention?_: To take into account the environment instability, an intention-persistence coefficient is applied: with this probability, the current intention is removed from the intention stack. 
1. _Do I have a current plan?_: If I have a current plan, just execute it. Similarly to intentions, a plan-persistence coefficient is defined: with this probability, the current plan is just dropped.
1. _Choose a desire as new current intention_: If the current intention is on hold (or the intention base is empty), choose a desire as new current intention. The new selected intention is the desire with higher priority.
1. _Choose a plan as a new current plan_: The new current plan is selected among the plans compatible with the current intention (and if their activation condition is checked) and with the highest priority.
1. _Execute the plan_: The current plan is executed.
1. _Is my plan finished?_: To allow persistent plans, a plan may have a termination condition. If it is not reached, the same plan will be kept for the next iteration.
1. _Was my plan instantaneous?_: Most multi-agent based simulation frameworks (GAMA included) are synchronous frameworks using steps. One consequence is that it may be useful to apply several plans during one single step. For example, if a step represents a day or a year, it would be unrealistic for an agent to spend one step to apply a plan like "choose a destination". This kind of plans (mostly reasoning plans) can be defined as instantaneous: in this case a new thinking loop is applied during the same agent step.


The architecture introduces two new main types of variables related to cognition: 
* **predicate**: a predicate unifies the representation of the information about the world. It can represent a situation, an event or an action. 

* **mental_state**: it represents the element (belief, desire, intention) manipulated by the agent and the architecture to take a decision. A mental state is composed of a modality, a predicate or another mental state, a real value and a lifetime. The modality indicates the type of the mental state (e.g. a belief or a desire), the predicate indicates the fact about which is this mental state (a mental state can also be about another mental state like a belief about a belief, etc), the value has a different interpretation depending on the modality and finally, the lifetime indicate the duration of the mental state (it can be infinite).

## Model Definition
### predicates
As a first step of the integration of the BDI agents in our model, we define a set of global predicate that will represent all the information that will be manipulated by the miner agents:
* _mine_location_: represents the information about the location of a gold mine.
* _has_gold_: represents the information that the miner has a gold nugget.
* _choose_goldmine_: represents the information that the miner wants to choose a gold mine
* _extract_gold_: represents the information that the miner wants to extract gold
* _find_gold_: represents the information that the miner wants to find gold
* _sell_gold_: represents the information that the miner wants to sell gold
```
global {
        ...
	predicate mine_location <- new_predicate(mine_at_location) ;
	predicate has_gold <- new_predicate("has gold");
	
	predicate choose_goldmine <- new_predicate("choose a gold mine");
	predicate extract_gold <- new_predicate("extract gold");
	predicate find_gold <- new_predicate("find gold") ;
	predicate sell_gold <- new_predicate("sell gold") ;
        ...
}
```	
### skeleton of the miner species
We then define a miner species with the _moving_ skill and the _simple_bdi_ control architecture. The miner agents have 5 variables:
* _viewdist_: distance of perception of the miner agent
* _speed_: speed of the agent
* _mycolor_: the color of the agent (random color)
* _target_: where the agent wants to go
* _gold_sold_: the number of gold nuggets sold by the agent

We define the init block of the species such as to add at the creation of the agent the desire to find gold nuggets (_find_gold_ predicate). we use for that the _add_desire_ action provides with the BDI architecture.

At last, we define an aspect in which we draw the agent with its _mycolor_ color and with a depth that depends on the number of gold nuggets collected.

```	
species miner skills: [moving] control:simple_bdi {
	float viewdist<-100.0;
	float speed <- 10.0;
	rgb mycolor<-rnd_color(255);
	point target;
	int gold_sold;
	
	init
	{
		do add_desire(find_gold);
	}
	aspect default {
	        draw circle(20) color: mycolor border: #black depth: gold_sold;
	}
}
```

### perception	
We add a perceive statement for the miner agents. This perceive will allow to detect the gold mine that are not empty

```
species miner skills: [moving] control:simple_bdi {
	...	
	perceive target:goldmine where (each.quantity > 0) in:viewdist {
		focus mine_at_location var:location;
		ask myself {
			do remove_intention(find_gold, false);
		}
	}
}
```
### rules
```
species miner skills: [moving] control:simple_bdi {
	...
	rule belief: mine_location new_desire: extract_gold strength: 2.0;
	rule belief: has_gold new_desire: sell_gold strength: 3.0;
}
```

### plans
```
species miner skills: [moving] control:simple_bdi {
        ...
        plan letsWander intention:find_gold 
	{
		do wander;
	}
       ...
}
```

```
species miner skills: [moving] control:simple_bdi {
        ...
        plan getGold intention:extract_gold 
	{
		if (target = nil) {
			do add_subintention(extract_gold,choose_goldmine, true);
			do current_intention_on_hold();
		} else {
			do goto target: target ;
			if (target = location)  {
				goldmine current_mine<- goldmine first_with (target = each.location);
				if current_mine.quantity > 0 {
				 	do add_belief(has_gold);
					ask current_mine {quantity <- quantity - 1;}	
				} else {
					do add_belief(new_predicate(empty_mine_location, ["location_value"::target]));
				}
				target <- nil;
			}
		}	
	}
       ...
}
```

```
species miner skills: [moving] control:simple_bdi {
        ...
        plan choose_closest_goldmine intention: choose_goldmine instantaneous: true{
		list<point> possible_mines <- get_beliefs_with_name(mine_at_location) collect (point(get_predicate(mental_state (each)).values["location_value"]));
		list<point> empty_mines <- get_beliefs_with_name(empty_mine_location) collect (point(get_predicate(mental_state (each)).values["location_value"]));
		possible_mines <- possible_mines - empty_mines;
		if (empty(possible_mines)) {
			do remove_intention(extract_gold, true); 
		} else {
			target <- (possible_mines with_min_of (each distance_to self)).location;
		}
		do remove_intention(choose_goldmine, true); 
	}
       ...
}
```

```
species miner skills: [moving] control:simple_bdi {
        ...
        plan return_to_base intention: sell_gold {
		do goto target: the_market ;
		if (the_market.location = location)  {
			do remove_belief(has_gold);
			do remove_intention(sell_gold, true);
			gold_sold <- gold_sold + 1;
		}
	}
       ...
}
```

## Complete Model

```
model GoldBdi

global {
	int nb_mines <- 10; 
	int nbminer<-5;
	market the_market;
	
	string mine_at_location <- "mine_at_location";
	string empty_mine_location <- "empty_mine_location";
	//possible beliefs of miners
	predicate mine_location <- new_predicate(mine_at_location) ;
	predicate has_gold <- new_predicate("has gold");
	
	//possible desires of miners
	predicate choose_goldmine <- new_predicate("choose a gold mine");
	predicate extract_gold <- new_predicate("extract gold");
	predicate find_gold <- new_predicate("find gold") ;
	predicate sell_gold <- new_predicate("sell gold") ;
	
	float inequality <- 0.0 update:standard_deviation(miner collect each.gold_sold);
	
	geometry shape <- square(2000);
	init
	{
		create market {
			the_market <- self;	
		}
		create goldmine number:nb_mines;
		create miner number:nbminer;
	}
	
	reflex end_simulation when: sum(goldmine collect each.quantity) = 0 and empty(miner where each.has_belief(has_gold)){
		do pause;
	}
}

species goldmine {
	int quantity <- rnd(1,20);
	aspect default
	{
		if (quantity = 0) {
			draw triangle(20) color: #gray border: #black;	
		} else {
			draw triangle(20 + quantity*5) color: #yellow border: #black;	
		}
	 
	}
}

species market {
	int golds;
	aspect default
	{
	  draw square(100) color: #black ;
	}
}

species miner skills: [moving] control:simple_bdi {
	
	float viewdist<-100.0;
	float speed <- 10.0;
	rgb mycolor<-rnd_color(255);
	point target;
	int gold_sold;
	
	init
	{
		do add_desire(find_gold);
	}
		
	perceive target:goldmine where (each.quantity > 0) in:viewdist {
		focus mine_at_location var:location;
		ask myself {
			do remove_intention(find_gold, false);
		}
	}
	rule belief: mine_location new_desire: extract_gold strength: 2.0;
	rule belief: has_gold new_desire: sell_gold strength: 3.0;
	
		
	plan letsWander intention:find_gold 
	{
		do wander;
	}
	
	plan getGold intention:extract_gold 
	{
		if (target = nil) {
			do add_subintention(extract_gold,choose_goldmine, true);
			do current_intention_on_hold();
		} else {
			do goto target: target ;
			if (target = location)  {
				goldmine current_mine<- goldmine first_with (target = each.location);
				if current_mine.quantity > 0 {
				 	do add_belief(has_gold);
					ask current_mine {quantity <- quantity - 1;}	
				} else {
					do add_belief(new_predicate(empty_mine_location, ["location_value"::target]));
				}
				target <- nil;
			}
		}	
	}
	
	plan choose_closest_goldmine intention: choose_goldmine instantaneous: true{
		list<point> possible_mines <- get_beliefs_with_name(mine_at_location) collect (point(get_predicate(mental_state (each)).values["location_value"]));
		list<point> empty_mines <- get_beliefs_with_name(empty_mine_location) collect (point(get_predicate(mental_state (each)).values["location_value"]));
		possible_mines <- possible_mines - empty_mines;
		if (empty(possible_mines)) {
			do remove_intention(extract_gold, true); 
		} else {
			target <- (possible_mines with_min_of (each distance_to self)).location;
		}
		do remove_intention(choose_goldmine, true); 
	}
	
	plan return_to_base intention: sell_gold {
		do goto target: the_market ;
		if (the_market.location = location)  {
			do remove_belief(has_gold);
			do remove_intention(sell_gold, true);
			gold_sold <- gold_sold + 1;
		}
	}

	aspect default {
	  draw circle(20) color: mycolor border: #black depth: gold_sold;
	}
}


experiment GoldBdi type: gui {

	output {
		display map type: opengl
		{
			species market ;
			species goldmine ;
			species miner;
		}
	}
}

experiment batch type: batch repeat: 30 until: sum(goldmine collect each.quantity) = 0 and empty(miner where each.has_belief(has_gold)) {
	float seed <- 100.0;
	reflex result {
		write "result mean time: " + mean(simulations collect each.cycle);
		write "result mean inequality: " + mean(simulations collect each.inequality);
	}
}
```