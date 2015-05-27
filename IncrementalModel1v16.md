
<br />
# <font color='blue'>Purpose</font>

This model illustrates how to create simple agent and make them move in their environment.

# <font color='blue'>Formulation</font>
  * Define a species A
  * Create 1000 instances of species A.

# <font color='blue'>Model</font>


## Entities
In this first model, we define one species of agents: the **A** agents.

For each of these species, we define a new attribute: **color** of type _rgb_, with a random initial value.

We define a reflex **moving\_around** that changes the location of the agent to any point in the world at each simulation step.

At last, we define an aspect for these species (see [Aspects](Species.md) in the Modeling guide). In this model, we want to represent the agent as a circle of radius 1, we then use the keyword **draw** that allows to draw a given shape/geometry. In order to draw a circle of radius 1, we use the operator **circle(1)**.


```
entities{
  species A{		
    rgb my_color<-rgb(rnd(255),rnd(255),rnd(255));
    
    reflex moving_around{
      location<- any_point_in(world.shape);
    }
 
    aspect my_aspect{
      draw circle(1) color:my_color;
    }
}
}
```





## Environment
We define a simple environment that is define by the enveloppe of 100 x 100 square

```
global {
  ...
  geometry shape<-envelope(square(100));; 
  ...
}
```

## Display
We define a display to draw agents. We use for that the classic **species** keyword.
In the **experiment** block:
```
output {
  display default_display{
    species A aspect:my_aspect;			
  }
}
```

# <font color='blue'>Complete model</font>

```

model model1

global{
  geometry shape<-envelope(square(100));
  init{
    create A number:1000;
  }
}

entities{
  species A{		
    rgb my_color<-rgb(rnd(255),rnd(255),rnd(255));
    reflex moving_around{
      location<- any_point_in(world.shape);
    }
    
    aspect my_aspect{
      draw circle(1) color:my_color;
    }
  }
}

experiment exp1 type:gui{
  output {
    display default_display{
      species A aspect:my_aspect;			
    }
  }
}
```