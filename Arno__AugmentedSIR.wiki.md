# Introduction

This tutorial shows how to augmented a simulation by using Gama Features. It supports online clustering events and produce dynamic traces of events that are represented by nodes and edges represent correlation both in time and space. It allows to trace the potential cause of emerging phenomenon and trace back their origin in the graph of event. This clustering algorithm is somewhat related to the one used in ClusteringSeer (http://www.biomedware.com/?module=Page&sID=clusterseer-overview).


We start from the following [Classical SIR Model](https://code.google.com/p/gama-platform/source/browse/branches/GAMA_CURRENT/msi.gama.models/models/Toy%20Models/Infection/Susceptible%20Infected%20Recovered%20(SIR).gaml)

![https://gama-platform.googlecode.com/svn/wiki/images/SIR.png](https://gama-platform.googlecode.com/svn/wiki/images/SIR.png)

# Study infectious process
From this model we like to study the infectious dynamic.

One of the first step is to isolate the infected agent and then to construct a network from those agent.

## Step 1: Abstraction

### Define Mirror Agent Species

```
species TraitAgent{
  aspect basic {
    draw sphere(1);
  }
}
```

### Create an Agent Mirror
Each time an agent becomes infected we create a mirror agent with the same location of the agent. This can easily be done in the reflex **become\_infected** of the agent.

In this reflex just add the creation of the mirror agent as follow

```
if (flip(beta * rate)) {
  ...
  create TraitAgent{
    color <- rgb(255,0,0);
    location <- myself.location;
  }   
}
```

### Display the agent
In the output don't forget to display the agent and place it (eventually) at a differet z position.
```
display sir_display{
  ..
  species TraitAgent aspect:basic position:{0,0,0.1};
}
```

You will obtain something like that

![https://gama-platform.googlecode.com/svn/wiki/images/SIR_Augmented.png](https://gama-platform.googlecode.com/svn/wiki/images/SIR_Augmented.png)

## Step 2: ???

### Add a time information on the color of the mirror agent
By simply using alpha channel we will give a visual information on the mirror agent.

#### Define an arrival time that will be automatically incremented every timestep
```
int arrivalTime update:arrivalTime+1;
```

#### Update the color of the mirror (the alpha part (the transparency) agent according to its arrival time
```
draw sphere(1) color: rgb(255,0,0,255-arrivalTime);
```

### Compute the neighbours of the mirror agent

#### Define a list of neighbours
```
list<TraitAgent> neighbours;
```

#### Update it in a reflex
```
reflex computeNeighbours {
  neighbours <- TraitAgent select ((each distance_to self) < 10);
}
```

#### Display the link between neighbours
```
loop pp over: neighbours {
  if(self.location!= pp.location){
    draw line([self.location,pp.location]) color:rgb('red');
  }	
}
```

The entire species
```
species TraitAgent{
  int arrivalTime update:arrivalTime+1;
  list<TraitAgent> neighbours;

  reflex computeNeighbours {
    neighbours <- TraitAgent select ((each distance_to self) < 10);
  }

  aspect basic {
    draw sphere(1) color: rgb(255,0,0,255-arrivalTime);
      loop pp over: neighbours {
        if(self.location!= pp.location){
	  draw line([self.location,pp.location]) color:rgb('red');
        }	
      }
  }
}
```

### Set the altitude of the agent according to its time apparition
Replace
```
create TraitAgent{
  location <- myself.location;
} 
```
by
```
create TraitAgent{
  location <-{myself.location.x,myself.location.y,time/10};
} 
```

## Step 3 : help yourself

<a href='http://www.youtube.com/watch?feature=player_embedded&v=bFBk8mzhtGI' target='_blank'><img src='http://img.youtube.com/vi/bFBk8mzhtGI/0.jpg' width='425' height=344 /></a>
