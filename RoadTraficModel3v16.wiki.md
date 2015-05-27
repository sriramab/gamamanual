
<br />
# <font color='blue'>Purpose</font>

Illustrates how to constrain the movement of an agent according to a network of polylines.

# <font color='blue'>Formulation</font>
  * Definition of day\_time global variable that will indicate, according to the simulation step, the time of the day: each simulation step will represent 10 minutes, then the day\_time variable will be ranged between 0 and 144.
  * For each **people** agent: define a living\_place(building of type 'Residential') and working place (building of type 'Industrial').
  * For each **people** agent: define start\_work and end\_work hours that repectively represent when the agent leaves its house to go to work and when it leaves its working\_place to go back home. These hours will be randomly define between 36 and 60 for the start\_work and 84 and 132 for the end\_work.
  * For each **people** agent: define a objective variable: this one can 'go home' or 'working'.
  * For each **people** agent: define a speed. The speed will be randomly define between 50 and 100.
  * The **people** agents move along the road, taking the shortest path.

# <font color='blue'>Model</font>

## People agents
First, we have to change the skill of the **people** agents: as we want to use an action of the **moving** skill (**goto**), we will provide the **people** agents with this skill.

```
   species people skills: [moving]{
       ...
   }
```

Then, we have to add new variables to the people agents: living\_place, working\_place, start\_work, end\_work, objective. In addition, we will add a "the\_target" variable that will represents the point toward which the agent is moving.

```
   species people skills: [moving]{
      rgb color <- rgb("yellow") ;
      building living_place <- nil ;
      building working_place <- nil ;
      int start_work ;
      int end_work  ;
      string objectif ; 
      point the_target <- nil ;
      
       ...
   }
```

We define two reflex methods that allow to change the objective (and the\_target) of the agent at the start\_work and en\_work hours. Concerning the _target value, we choose a random point in the objective building (working\_place or living\_place) by using the **any\_location\_in** operator._

```
   species people skills: [moving]{  
      ...
      reflex time_to_work when: day_time = start_work {
         objectif <- "working" ;
         the_target <- any_location_in (working_place);
      }
      reflex time_to_go_home when: day_time = end_work {
         objectif <- "go home" ;
         the_target <- any_location_in (living_place); 
      }  
      ...
   }
```

At last, we define a reflex method that allows the agent to move. If a target point is defined (the\_target != nil), the agent moves in direction to its target using the **goto** action. Note that we specified a graph to constraint the moving of the agents on the road network with the facet **on**. We will see later how this graph is built. When the agent arrives at destination (the\_target = location), the target is set to nil (the agent will stop moving).

```
  species people skills: [moving]{
      ...
      reflex move when: the_target != nil {
         do goto (target: the_target on: the_graph) ; 
         switch the_target { 
            match location {the_target <- nil ;}
         }
      }
   }
```

## Parameters
We add several parameters (**min\_work\_start**, **max\_work\_start**, **min\_work\_end**, **max\_work\_end**, **min\_speed** and **max\_speed**) and two global variables: **the\_graph** (graph computed from the road network) and **day\_time** (current time of the day). The value of the **day\_time** variable is automatically computed at each simulation step and is equals to "cycle (the simulation step) modulo 144" (one day is decomposed in 144 simulation steps).

In the global section:
```
global {
    ...
   int min_work_start <- 36;
   int max_work_start <- 60;
   int min_work_end <- 84; 
   int max_work_end <- 132; 
   float min_speed <- 50.0;
   float max_speed <- 100.0; 
   int day_time <- 0 update: cycle mod 144 ;
   graph the_graph;
    ...
}
```

In the experiment section:
```
experiment road_traffic type: gui {
      ... 
   parameter "Earliest hour to start work" var: min_work_start category: "People" ;
   parameter "Latest hour to start work" var: max_work_start category: "People" ;
   parameter "Earliest hour to end work" var: min_work_end category: "People" ;
   parameter "Latest hour to end work" var: max_work_end category: "People" ;
   parameter "minimal speed" var: min_speed category: "People" ;
   parameter "maximal speed" var: max_speed category: "People" ;
    ...
}
```
## Initialisation
First, we need to compute from the **road** agents, a graph for the moving of the **people** agents. The operator **as\_edge\_graph** allows to do that. It automatically builds from a set of agents or geometries a graph where the agents are the edges of the graph, a node represent the extremities of the agent geometry.
```
   init {
      ...
      create road from: shape_file_roads ;
      the_graph <- as_edge_graph(road);
      ...
   }
```

We randomly assign one working place and one house to each **people** agent. To simplify the GAML code, we define two temporary variables: the list of buildings of type 'Residential' and the list of buildings of type 'Industrial' (by using the **where** command). At the creation of each **people** agent, we define a speed, a start\_work and end\_work to each **people** agent (according to the min and max define in the parameters). Concerning the definition of the living\_place and working\_place, these ones are randomly chosen in the residential\_buildings and industrial\_buildings lists.
```
   init {
      ...
      list<building> residential_buildings <- building where (each.type="Residential");
      list<building> industrial_buildings <- building where (each.type="Industrial") ;
      create people number: nb_people {
         speed <- min_speed + rnd (max_speed - min_speed) ;
         start_work <- min_work_start + rnd (max_work_start - min_work_start) ;
         end_work <- min_work_end + rnd (max_work_end - min_work_end) ;
         living_place <- one_of(residential_buildings) ;
         working_place <- one_of(industrial_buildings) ;
         location <- any_location_in (living_place); 
      }
      ...
   }
```

# <font color='blue'>Complete model</font>

# <font color='blue'>Complete model</font>

```
model tutorial_gis_city_traffic

global {
   file shape_file_buildings <- file("../includes/building.shp");
   file shape_file_roads <- file("../includes/road.shp");
   file shape_file_bounds <- file("../includes/bounds.shp");
   geometry shape <- envelope(shape_file_bounds);
   int nb_people <- 100;
   init {
       create building from: shape_file_buildings with: [type::read ('NATURE')] {
         if type="Industrial" {
            color <- rgb("blue") ;
         }
      }
      create road from: shape_file_roads ;
      the_graph <- as_edge_graph(road);
      list<building> residential_buildings <- building where (each.type="Residential");
      list<building> industrial_buildings <- building where (each.type="Industrial") ;
      create people number: nb_people {
         speed <- min_speed + rnd (max_speed - min_speed) ;
         start_work <- min_work_start + rnd (max_work_start - min_work_start) ;
         end_work <- min_work_end + rnd (max_work_end - min_work_end) ;
         living_place <- one_of(residential_buildings) ;
         working_place <- one_of(industrial_buildings) ;
         location <- any_location_in (living_place); 
      }
   }
}
entities {
   species building {
      string type; 
      rgb color <- rgb("gray")  ;
      aspect base {
         draw shape color: color ;
      }
   }
   species road  {
      rgb color <- rgb("black") ;
      aspect base {
         draw shape color: color ;
      }
   }
    species people skills: [moving]{
      rgb color <- rgb("yellow") ;
      building living_place <- nil ;
      building working_place <- nil ;
      int start_work ;
      int end_work  ;
      string objectif ; 
      point the_target <- nil ;
     
      reflex time_to_work when: day_time = start_work {
         objectif <- "working" ;
         the_target <- any_location_in (working_place);
      }
      reflex time_to_go_home when: day_time = end_work {
         objectif <- "go home" ;
         the_target <- any_location_in (living_place); 
      }  
      reflex move when: the_target != nil {
         do goto (target: the_target on: the_graph) ; 
         switch the_target { 
            match location {the_target <- nil ;}
         }
      }
      
      aspect base {
         draw circle(10) color: color ;
      }
   }
}
   
experiment road_traffic type: gui {
   parameter "Shapefile for the buildings:" var: shape_file_buildings category: "GIS" ;
   parameter "Shapefile for the roads:" var: shape_file_roads category: "GIS" ;
   parameter "Shapefile for the bounds:" var: shape_file_bounds category: "GIS" ; 
   parameter "Number of people agents" var: nb_people category: "People" ;
   parameter "Earliest hour to start work" var: min_work_start category: "People" ;
   parameter "Latest hour to start work" var: max_work_start category: "People" ;
   parameter "Earliest hour to end work" var: min_work_end category: "People" ;
   parameter "Latest hour to end work" var: max_work_end category: "People" ;
   parameter "minimal speed" var: min_speed category: "People" ;
   parameter "maximal speed" var: max_speed category: "People" ;
   output {
      display city_display {
         species building aspect: base ;
         species road aspect: base ;
         species people aspect: base ;
      }
   }
}
```