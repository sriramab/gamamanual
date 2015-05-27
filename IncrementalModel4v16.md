
<br />
# <font color='blue'>Purpose</font>

This model illustrates how to create a social graph between agents.

# <font color='blue'>Formulation</font>
  * Create a friend ship graph

# <font color='blue'>Model</font>


## Entities
  * Creation of the species **people**
The species people has an attribute **my\_color** of type _rgb_ randomly initialized. An attribute **location** of type _point_ that is initialized thanks to the operator [any\_location\_in](#any_location_in.md) to any places on one of the roads.
The species people has a moving skill (more details here # [Movement of the people agents](RoadTraficModel3v16.md)) and can thus move on the road to a given **target** at a given **speed**

The species people is represented by a circle whose size depend on the degree of the people (using [degree\_of](#degree_of.md) operator) in the **friendship\_graph**


```
species people skills: [moving]{
  rgb my_color<-rgb(rnd(2)*120,rnd(1)*250,rnd(2)*120);
  point location <- any_location_in(one_of(road));
  people target<- one_of(people);
  float size ;
		
  action updateSize {
    size <- friendship_graph degree_of (self);
  }

  reflex movement {
    if (location distance_to target < 5.0) {
      target <- one_of(people);
      do updateSize;
    }
    do goto on:road_graph target:target speed:1 + rnd(2);
  }
  
  aspect base {
    draw circle(size) color:my_color;
  }
}
```


  * Creation of a new species **friendship\_link** that represents the relationship between two people.
The agent friendship\_link is represented by its shape in the aspect **base**

```
species friendship_link {
  aspect base {
    draw shape color: rgb('black') ;			
  }
}
```





## Graph creation
Gama offers different generator of graph. In this example we are using [generate\_barabasi\_albert](#generate_barabasi_albert.md)
```
init {
...
friendship_graph <- generate_barabasi_albert(people,friendship_link,100,1);	
}
```



# <font color='blue'>Complete model</font>

```
model multigraph

global {
  file shape_file_in <- file('../includes/road.shp') ;
  file shape_file_bounds <- file('../includes/bounds.shp') ;
  geometry shape <- envelope(shape_file_bounds);

  graph road_graph; 
  graph friendship_graph;
	
  init {
  
    //Road graph creation
    create road from: shape_file_in;
    road_graph <- as_edge_graph(road);
		
    //Friendship graph creation 
    friendship_graph <- generate_barabasi_albert(people,friendship_link,100,1);		
  }
}

entities {
species people skills: [moving]{
  rgb my_color<-rgb(rnd(2)*120,rnd(1)*250,rnd(2)*120);
  point location <- any_location_in(one_of(road));
  people target<- one_of(people);
  float size ;
		
  action updateSize {
    size <- friendship_graph degree_of (self);
  }

  reflex movement {
    if (location distance_to target < 5.0) {
      target <- one_of(people);
      do updateSize;
    }
    do goto on:road_graph target:target speed:1 + rnd(2);
  }
  
  aspect base {
    draw circle(size) color:my_color;
  }
}

species friendship_link {
  aspect base {
    draw shape color: rgb('black') ;			
  }
}
species road  {
	aspect base {
		draw shape color: rgb('black') ;
	}
}
}

experiment multigraph type: gui {
  output {
    display friendship {
      species road aspect: base;
      species friendship_link aspect: base;
      species people aspect: base;
    }
  }
}
```