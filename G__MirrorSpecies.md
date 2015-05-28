# Mirror Species (Under Construction)
<font color='red'><i>todo</i>:<br>
<ul><li>explain the population management a little bit more in details<br>
</li><li>explain the constraints (no mirror of itself, no 'create', no reciprocal mirrors — otherwise problems)<br>
</font>
<hr />
A <b>mirror</b> species is a species whose population is automatically managed with respect to another species. Whenever an agent is created or destroyed from the other species, an instance of the <b>mirror</b> species is created or destroyed.  Each of these  'mirror agents' has access to its reference agent (called its <b>target</b>).</li></ul>

**Mirror** species can be used in different situations but the one we describe here is more oriented towards visualization purposes.







## Declaration

Given any already declared species
```
species A {
...
}
```

A mirror species can be defined using the **mirrors** keyword as following:

```
species B mirrors: A{
}
```

In this case the species B mirrors the species A.

By default the location of the species B will be random but in many cases, once want to place the mirror agent at the same location of the reference species. This can be achieve by simply adding the following lines in the mirror species

```
point location <- target.location update: target.location;
```

In the same spirit any attribute of a reference species can be reach using the same syntax. For instance if the species A has an attribute called _attribute1_ of type _int_ is is possible to get this attribute from the mirror species B using the following syntax:

```
int value <- target.attribute1;
```

## Example
This model simply instantiates 100 agents of the species A that has a moving skills and are wandering at each step.

On top of this species a mirror species B is created.

```
model Mirror

global {
  init{
    create A number:100;	
  }
}

species A skills:[moving]{
	reflex update{
		do wander;
	}
	aspect base{
		draw circle(1) color: #white;
	}
}
species B mirrors: A{
	point location <- target.location update: target.location;
	aspect base {
		draw sphere(2) color: #blue;
	}
}

experiment mirroExp type: gui {
	output {
		display superposedView type: opengl{ 
		  species A aspect: base;
		  species B aspect: base transparency:0.5;
		}
	}
}
```