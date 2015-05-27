# Graph Species (Under Construction)
<font color='red'><i>todo</i>:<br>
<ul><li>make references to the topology and maybe better explain the purpose of 'graph' species: build a graph using agents (and not — only — between agents).<br>
</li><li>link with the two built-in species mentioned<br>
</li><li>give constraints (no other topology can be defined)<br>
</font>
<hr />
Using a <b>graph</b> species enables to easily shows interaction between agent of a same species. This kind of species is particularly useful when trying to show the interaction (especially the non spatial one) that exist between agent.</li></ul>

To instantiate this **graph** species, several step must be followed. First the graph species must inherit from the abstract species **graph\_node**, then the method **related\_to** must be redefined and finally an auxiliary species that inherits from **base\_edge** used to represent the edges of the generated graph must be declared.

A **graph node** is an abstract species that must redefine one method called **related\_to**. This method returns true or false according to a given condition that will express the distance between two agents. This distance can be of course the euclidean distance (but in this case it is recommenced to use the operator [as\_distance\_graph](G__OperatorsAK#as_distance_graph.md) but also any other distance define by the user.


<br />

---

## Declaration

```
species A parent: graph_node edge_species: edge_agent{
  bool related_to(A other){
  using topology(world) {
      return (self.location distance_to other.location) < 10;
  }
  }
}
```

Define the species used to represent the edges of the generated graph
```
species edge_agent parent: base_edge {
  aspect base {
    draw shape color: rgb("green");
  }
}
```




## Example


```
model GraphSpecies

global {
  init{
    create A number:100;	
  }
}
species A parent: graph_node edge_species: edge_agent{

	bool related_to(A other){
		using topology(world){
			return (self.location distance_to other.location) < 10;
		}	
	}
	aspect base {
		draw sphere(1) color: #blue;
	}
}

species edge_agent parent: base_edge {
	rgb color;
	aspect base {
		draw shape color: rgb("green");
	}
}

experiment graphExp type: gui {
	output {
		display graphView type: opengl{
		  species A aspect: base;
		  species edge_agent aspect:base;
		}
	}
}
```