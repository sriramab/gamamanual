
<br />
# <font color='blue'>Purpose</font>

Illustrates how to display charts.

# <font color='blue'>Formulation</font>
  * Add a chart to display the evolution of the road destruction: the mean value of the **destruction\_coeff** of the **road** agents, and its max value (refreshed every 10 simulation steps).
  * Add a chart to display the activity of the **people** agent (working or staying home, refreshed every 10 simulation steps).

# <font color='blue'>Model</font>

## Chart display
First we add a chart of type **series** to display the road destruction evolution. To compute the mean of the **destruction\_coeff**, we use the **mean** operator. For the max, we use the **max\_of** operator.

```
     output {
       display chart_display refresh_every: 10 {
         chart "Road Status" type: series background: rgb("lightGray") size: {0.9, 0.4} position: {0.05, 0.05} {
            data "Mean road destruction" value: mean (road collect each.destruction_coeff) style: line color: rgb("green") ;
            data "Max road destruction" value: road max_of (each.destruction_coeff) style: line color: rgb("red") ;
         }
         ...
      }
   }
```

Second, we add a chart of type **pie** to display the activity of the **people** agents. We use for that the **objective** variable of the **people** agents and the **count** operator that allows to compute the number of elements of a list that verify a condition.

```
    output {
      ...
      display chart_display refresh_every: 10 {
        ...
        chart "People Objectif" type: pie background: rgb("lightGray") style: exploded size: {0.9, 0.4} position: {0.05, 0.55} {
            data "Working" value: people count (each.objective="working") color: rgb('green') ;
            data "Staying home" value: people count (each.objective="go home")) color: rgb("blue") ;
       }
     }
   }
```

# <font color='blue'>Complete model</font>

```
model tutorial_gis_city_traffic

global {
   file shape_file_buildings <- file("../includes/building.shp");
   file shape_file_roads <- file("../includes/road.shp");
   file shape_file_bounds <- file("../includes/bounds.shp");
   geometry shape <- envelope(shape_file_bounds);
   int nb_people <- 100;
   float destroy <- 0.02;
   init {
       create building from: shape_file_buildings with: [type::read ('NATURE')] {
         if type="Industrial" {
            color <- rgb("blue") ;
         }
      }
      create road from: shape_file_roads ;
      map<road,float> weights_map <- road as_map (each:: (each.destruction_coeff * each.shape.perimeter));
      the_graph <- as_edge_graph(road) with_weights weights_map;
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
      reflex update_graph{
         map<road,float> weights_map <- road as_map (each:: (each.destruction_coeff * each.shape.perimeter));
         the_graph <- the_graph with_weights weights_map;
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
      float destruction_coeff <- 1.0  max: 2.0;
      int colorValue <- int(255*(destruction_coeff - 1)) update: int(255*(destruction_coeff - 1)) min: 0 max: 255;
      rgb color <- rgb(colorValue,255 - colorValue,0)  update: rgb(colorValue,255 - colorValue,0);
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
         path path_followed <- goto (target:the_target, on:the_graph, return_path: true);
         list<geometry> segments <- path_followed.segments;
         loop line over: segments {
            float dist <- line.perimeter;
            road the_road<- road(path_followed agent_from_geometry line); 
            ask the_road {
               destruction_coeff <- destruction_coeff + (destroy * dist / shape.perimeter);
            }
         }
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
   parameter "Value of destruction when a people agent takes a road" var: destroy category: "Road" ;
   output {
      display city_display {
         species building aspect: base ;
         species road aspect: base ;
         species people aspect: base ;
      }
      display chart_display refresh_every: 10 {
         chart "Road Status" type: series background: rgb("lightGray") size: {0.9, 0.4} position: {0.05, 0.05} {
            data "Mean road destruction" value: mean (road collect each.destruction_coeff) style: line color: rgb("green") ;
            data "Max road destruction" value: road max_of (each.destruction_coeff) style: line color: rgb("red") ;
         }
         chart "People Objectif" type: pie background: rgb("lightGray") style: exploded size: {0.9, 0.4} position: {0.05, 0.55} {
            data "Working" value: people count (each.objective="working") color: rgb('green') ;
            data "Staying home" value: people count (each.objective="go home")) color: rgb("blue") ;
        }
   }
}
```