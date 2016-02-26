[//]: # (keyword|operator_round)
[//]: # (keyword|operator_sort_by)
[//]: # (keyword|operator_last)
[//]: # (keyword|operator_line)
[//]: # (keyword|operator_font)
[//]: # (keyword|operator_distance_between)
[//]: # (keyword|operator_with_precision)
[//]: # (keyword|operator_copy)
[//]: # (keyword|operator_triangle)
[//]: # (keyword|skill_fsm)
[//]: # (keyword|type_topology)
[//]: # (keyword|type_species)
[//]: # (keyword|statement_state)
[//]: # (keyword|statement_transition)
[//]: # (keyword|statement_diffuse)
[//]: # (keyword|statement_agents)
[//]: # (keyword|statement_inspect)
[//]: # (keyword|statement_exhaustive)
[//]: # (keyword|statement_permanent)
[//]: # (keyword|statement_genetic)
[//]: # (keyword|statement_event)
[//]: # (keyword|architecture_fsm)
[//]: # (keyword|constant_zoom)
[//]: # (keyword|constant_bold)
[//]: # (keyword|constant_plain)
[//]: # (keyword|constant_darkgray)
[//]: # (keyword|constant_darkgreen)
[//]: # (keyword|constant_lightblue)
[//]: # (keyword|concept_Comodel)
# ComodelAntsBoids


_Author : hqnghi_

Co-model example : coupling Ants and Boids. In an experimental use case, Boids chase and eat Ants when Ants are trying to fill-up their nids.


```
  
model comodelAnts
import "../../../Toy Models/Ants (Foraging and Sorting)/models/Ant Foraging (Complex).gaml" as myAnt
import "../../../Toy Models/Boids/models/Boids.gaml" as myBoids
global {
	geometry shape<-envelope(500);
	
	init{
		create myBoids.boids_gui with:[shape::circle(5),width_and_height_of_environment::500,number_of_agents::20];
		create myAnt.Complete with:[gridsize::100,ants_number::100];
	}
	reflex dododo{
		
		
		ask (myAnt.Complete){
			do _step_;
		}
		ask (myBoids.boids_gui){
			do _step_;
		}
	}
}

experiment comodelExp_Ants_Boids type: gui {
	
	output {
		display "comodel_disp" {			
			image 'background' file:'../images/soil.jpg';
			species species((first(myBoids.boids_gui).simulation.boids)[0]) aspect: image;
			agents "agents_ant_grid" transparency: 0.5 position:point((first(myBoids.boids_gui).simulation.boids_goal)) value: (first(myAnt.Complete).simulation.ant_grid as list) where ((each.food > 0) or (each.road > 0) or (each.is_nest));
			agents "agents_ant" aspect:icon value:first(myAnt.Complete).simulation.ant  position:point((first(myBoids.boids_gui).simulation.boids_goal));
			
			agents "agents_bois" aspect:image value:first(myBoids.boids_gui).simulation.boids;//  position:(first(myBoids.Boids2).simulation.boids_goal); 

		} 
	}
	
}
```
