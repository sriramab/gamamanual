
<br />
# <font color='blue'>Purpose</font>

Illustrates how to add weights to a network of polylines.

# <font color='blue'>Formulation</font>
  * Add a **destruction\_coeff** variable to the **road** agent. The value of this variable is higher or equal to 1 or lower or equal to 2. At initialisation, the value of this variable is randomly defined between 1 and 2.
  * In the road network graph, more a road is worn out (destruction\_coeff high), more a **people** agent takes time to go all over it. Then the value of the arc representing the road in the graph is equal to "length of the road `*` destruction\_coeff".
  * The color of the road depends of the **destruction\_coeff**. If "destruction\_coeff = 1", the road is green, if "destruction\_coeff = 2", the road is red.


# <font color='blue'>Model</font>


## Road agent
We add a **destruction\_coeff** variable which initial value is randomly defined between 1 and 2 and that have a max of 2. The color of the agent will depend of this variable. In order to simplify the GAML code, we define a new variable  **colorValue** that represents the value of red color and that will be defined between 0 and 255.

```
   species road  {
      float destruction_coeff <- 1 + ((rnd(100))/ 100.0) max: 2.0;
      int colorValue <- int(255*(destruction_coeff - 1)) update: int(255*(destruction_coeff - 1)) min: 0 max: 255;
      rgb color <- rgb(colorValue,255 - colorValue,0)  update: rgb(colorValue,255 - colorValue,0);
      ...
   }
```


## Weigthed road network
In GAMA, adding a weight for a graph is very simple, we just have to use the **as\_edge\_graph** operator with the graph for left-operand and a weight map for the right-operand. A weight contains the weight of each edge: [edge1::weight1, edge2:: weight2,...]. In this model, the weight will be equal to the length of the road (perimeter of the polyline) **its destruction coefficient.
```
    init {
      ...
      create road from: shape_file_roads ;
      map<road,float> weights_map <- road as_map (each:: (each.destruction_coeff * each.shape.perimeter));
      the_graph <- as_edge_graph(road) with_weights weights_map;
      ...
   }
```**

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
      float destruction_coeff <- 1 + ((rnd(100))/ 100.0)  max: 2.0;
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