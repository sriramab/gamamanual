[//]: # (keyword|architecture_fsm)
[//]: # (keyword|operator_min_of)
[//]: # (keyword|operator_sort)
[//]: # (keyword|operator_last)
[//]: # (keyword|operator_contains)
[//]: # (keyword|statement_state)
[//]: # (keyword|statement_transition)
[//]: # (keyword|statement_diffuse)
[//]: # (keyword|statement_datalist)
[//]: # (keyword|skill_fsm)
[//]: # (keyword|constant_orange)
[//]: # (keyword|constant_violet)
[//]: # (keyword|concept_gui)
[//]: # (keyword|concept_skill)
[//]: # (keyword|concept_grid)
# Ant Foraging (Charts examples)


_Author : _

Toy Model ant using the question of how ants search food and use pheromons to return to their nest once they did find food. In this model, the charts are particularly used.


Code of the model : 

```
model ants

global {
	//Number of ants
	int ants_number <- 100 min: 1 max: 2000 ;
	//Evaporation value per cycle for the pheromons
	float evaporation_per_cycle <- 5.0 min: 0.0 max: 240.0 ;
	//Diffusion rate for the pheromons
	float diffusion_rate <- 1.0 min: 0.0 max: 1.0 ;
	bool use_icons <- true ;
	bool display_state <- true;
	//Size of the grid
	int gridsize <- 75 ;
	//Center of the grid to put the location of the nest
	const center type: point <- { (gridsize / 2),  (gridsize / 2)} ;
	const types type: file <- (pgm_file('../images/environment75x75.pgm')) ;
	const ant_shape_empty type: string <- '../icons/ant.png' ;
	const ant_shape_full type: string <- '../icons/full_ant.png'  ;
	const C00CC00 type: rgb <- rgb('#00CC00') ;    
	const C009900 type: rgb <- rgb('#009900') ; 
	const C005500 type: rgb <- rgb('#005500') ; 
	int food_gathered <- 0 ;   
	geometry shape <- square(gridsize);
	init{  
		//Ant are placed randomly in the nest
		create ant number: ants_number with: [location::any_location_in (ant_grid(center))] ;
	}
	
	//Reflex to diffuse the road of pheromon on the grid
	reflex diffuse {
      diffuse var:road on:ant_grid proportion: diffusion_rate radius:2 propagation: gradient;
   }

}

//Grid to discretize space for the food and the nest
grid ant_grid width: gridsize height: gridsize neighbors: 8 use_regular_agents: false {
	bool multiagent <- true ;
	float road <- 0.0 max:240.0 update: (road<=evaporation_per_cycle) ? 0.0 : road-evaporation_per_cycle;
	int type <- int(types at {grid_x,grid_y}) ;
	bool isNestLocation <- (self distance_to center) < 4 ; 
	bool isFoodLocation <- type = 2 ; 
	rgb color <- isNestLocation ? °violet:((food > 0)? °blue : ((road < 0.001)? rgb ([100,100,100]) : ((road > 2)? °white : ((road > 0.5)? (C00CC00) : ((road > 0.2)? (C009900) : (C005500)))))) update: isNestLocation ? °violet:((food > 0)? °blue : ((road < 0.001)? rgb ([100,100,100]) : ((road > 2)? °white : ((road > 0.5)? (C00CC00) : ((road > 0.2)? (C009900) : (C005500)))))) ;
	int food <- isFoodLocation ? 5 : 0 ;
	const nest type: int <- 300 - int(self distance_to center) ;
	
}
//Species ant that will move and follow a final state machine
species ant skills: [moving] control: fsm {
	float speed <- 2.0 ;
	ant_grid place update: ant_grid (location ); 
	string im <- 'ant_shape_empty' ;
	bool hasFood <- false ;
	reflex diffuse_road when:hasFood=true{
      ant_grid(location).road <- ant_grid(location).road + 100.0;
   }
   //Action to pick food

	
	//Experiment with only two display : the grid and the ants, and a chart
	experiment AntOneDisp type: gui {
	parameter 'Number of ants:' var: ants_number category: 'Model' ;
	parameter 'Evaporation of the signal unit/cycle):' var: evaporation_per_cycle category: 'Model' ;
	parameter 'Rate of diffusion of the signal (%/cycle):' var: diffusion_rate category: 'Model' ;
	parameter 'Use icons for the agents:' var: use_icons category: 'Display' ;
	parameter 'Display state of agents:' var: display_state category: 'Display' ;

	list<list<int>> nbants<-[[0]];
	list<string> statesnames<-[""];
	list<string> categnames<-["empty","carry"];
	list<list<int>> nbantsbydist<-[[0]];
	list xytestvallist<-[[[1,1],[2,2],[3,3]],[[1,2],[2,1],[3,4]],[[1,3],[2,3],[0,1]],[[1,4],[2,5],[0,0]]];
	list<list<int>> xyval<-[[1,1],[2,1],[3,2]];

	reflex update_charts
	{
		ant x<-one_of(world.ant);
		loop x over:list(world.ant)
		{
			if !(statesnames contains (x.state))
			{				
			add [(list(ant) count (each.state=x.state and !each.hasFood)),(list(ant) count (each.state=x.state and each.hasFood))] to: nbants;
			add (x.state) to:statesnames;				
			int d<-0;
			list<int> nl<-[];
			loop d from:0 to:9
				{
			add (list(ant) count (each.state=x.state and (((each distance_to center)>gridsize/20*d) and ((each distance_to center)<gridsize/20*(d+1))))) to: nl;
				}
			add nl to:nbantsbydist;
			}
//			add length((list(world.ant) collect (each.next_place distance_to each.location)) where (each=x)) to:nbants;
		}
		write("nbants"+nbants);
		write("nbantsbydist"+nbantsbydist);
		write("states"+statesnames);		
	}
	output {
		display Ants type: opengl {
			grid ant_grid ;
			species ant aspect: text ;
		}

		display ChartSerieList {
			chart "DataListScatterHistory" type:scatter
			{
				datalist ["empty","carry"] value:[mean((list(ant) where (!each.hasFood)) collect each.location),mean((list(ant) where (each.hasFood)) collect each.location)]
					 color:[°red,°green] line_visible:true;				
			}
		}
	}
}


```
