# Install
You need to run the SVN version.

The plugin need to be add doing the following:

  * In ummisco.gama.feature.core open the feature.xml file.
  * In plug-ins click add the msi.gaml.architecture.simplebdi

# Acteur Projet
A website (still in construction) of the ACTEUR project can be found here http://acteur-anr.fr/


# An introduction to cognitive agent

The belief–desire–intention software model (usually referred to simply, but ambiguously, as BDI) is a software model developed for programming intelligent agents.

  * **Belief**: State of the agent.
  * **Desire**: Objectives that the agent would like to accomplish.
  * **Intention**: What the agent has chosen to do.
    * **Plan**: Sequences of actions that an agent can perform to achieve one or more of its intensions.

# Basic Example: A fire rescue model using cognitive agent

We introduce a simple example to illustrate the use of the BDI architecture.

This simple model consists in creating "cognitive" agent whose goal is to extinguish a fire. In a first approximation we consider only one static water area and fire area. The aim is not to have a realistic model but to illustrate how to give a "cognitive" behavior to an agent using the BDI architecture.

First let's create a BDI agent using the key control **simple\_bdi** (A description of all existing control architectures is available [here](G__BuiltInControlArchitectures).)

## Species Helicopter creation

```
species helicopter control: simple_bdi{
...
}
```

### Attributes
The species `helicopter` needs 3 attributes to represent the water value, its speed and a boolean to know if the target fire is extinguish or not.
```
float waterValue;
float speed <- 10.0;
bool target_fire_extinguish <- false;
```

### Predicates
The predicate are the structure that are used to define a belief, a desire or intention.
In this model we need 4 different predicates.


```
predicate patrol_desire <- new_predicate("patrol") with_priority 1;
predicate fire_predicate <- new_predicate("fire") ;
predicate water_predicate <- new_predicate("has water", true) with_priority 3;
predicate no_water_predicate <- new_predicate("has water", false) ;
```

### Initialization
The initialization consists in setting the attribute **waterValue** to 1 and to add one belief and one desire. Two optional parameters are also set. The first belief added is the **water\_predicate** saying that the helicopter has some water in is tank. And then the first desire added in the desire base is the **patrol\_desire** saying that the helicopter wants to patrol.
```
waterValue <-1.0;
do add_belief(water_predicate);
do add_desire(patrol_desire );
intention_persistence <- 0.0;
plan_persistence<-0.5;	
```

### Reflex
At each iteration the helicopter is checking if he has a fire in its neighborhood. It it's the case and if he did not find this fire then he will update its belief and desire. First he will add the belief that the current Fire is not yet extinguished, then he will add the desire to extinguish it and he will remove the intention to patrol.
```
reflex perception {
  loop fire over: fireArea at_distance 10 {
    if (not has_belief(new_predicate("fire", fire.location))) {
      do add_belief(new_predicate("fire", fire.location, ["extinguish"::false], 2));		
      do add_desire(new_predicate("fire", fire.location, ["extinguish"::true], 2));
      do remove_intention(patrol_desire,false);		
    }
  }	
}
```

### Plan
#### Patrolling
```
plan patrolling when: is_current_intention(patrol_desire) finished_when: has_belief(fire_predicate){
  do wander;
}
```
#### fallBack
Applied when the objective is to stop the fire but there is no more water. The current intention is put on hold and then a sub intention is added
```
plan stopFire when: (is_current_intention(fire_predicate) and has_belief(no_water_predicate)) finished_when: true piority:10
{
  do add_subintention(get_current_intention(), water_predicate);
  do add_desire(water_predicate);
  do current_intention_on_hold();	
}
```
#### stopFire
```
plan stopFire when: is_current_intention(fire_predicate) finished_when: target_fire_extinguish or has_belief(no_water_predicate){
predicate current_fire <- get_current_intention();
point target_fire <- point(current_fire.value );
if (self distance_to target_fire < 1) {
  fireArea current_fire <- fireArea first_with (each.location = target_fire);
  if (current_fire != nil) {
    waterValue <- waterValue - 0.5;
    if (waterValue = 0) {
      do remove_belief(water_predicate);
      do add_belief(no_water_predicate);
      do add_desire(water_predicate); 
    }
    current_fire.size <-  current_fire.size - 1;
    if ( current_fire.size = 0) {
      ask  current_fire {do die;}
      do remove_belief(new_predicate("fire", target_fire, ["extinguish"::false], 2));
      do remove_intention(fire_predicate,true);
      target_fire_extinguish <- true;
					
    }	else {
          target_fire_extinguish <- false;
    }	
   }			
} else {
  do goto target: target_fire;
}
}
```
#### gotoTakeWater
```
plan gotoTakeWater when: is_current_intention(water_predicate) finished_when: has_belief(water_predicate) {
    	waterArea wa <- first(waterArea);
    	do goto target: wa ;
    	if (self distance_to wa < 1) {
    		waterValue <- waterValue + 1.0;
    		wa.size <- wa.size - 1.0;
    		if ( wa.size = 0) {
				ask  wa {do die;}
			}
			do add_belief(water_predicate);	
			do remove_belief(no_water_predicate);	
			do remove_intention(water_predicate,true);
		}
        }
```