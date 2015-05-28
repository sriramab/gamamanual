# Defining equations (Under Construction)
<font color='red'><i>todo</i>:<br>
<ul><li>proofread the language (difficult to read sometime)<br>
</li><li>give more examples and explain the meaning of the "built-in" equations<br>
</li><li>link with the recipe on how to use equations<br>
</font>
<hr /></li></ul>

This extension of GAMA is some new statements that provides new way to write Math models (System of equations) and new action to solve them with provided method (RK4, Dormand,...). This extension is implemented in the ummisco.gaml.extensions.maths plug-in.






## Equations

### Define equation(s)

Example of declaration:
```
species Maths {
   float t;
   float S;
   float I;
   float R;

   equation SIR { 
      diff(S,t) = (- beta * S * I / N);
      diff(I,t) = (beta * S * I / N) - (alpha * I);
      diff(R,t) = (alpha * I);
   }

   ...
}   
```

diff keyword, for instant, is a place-holder for a syntax more Mathematically. Its first parameter is the variable, the second (variable t) will not change during solve process.

### Optional mode
#### simultaneously : [list of agents ]()
  * simultaneously mode which accept a list of agent contains equations. The Solve statement will compute simultaneously at same time all the equations

Example of declaration:
```
   species S_Maths {
      float S;
      equation eq simultaneously: [ I , first ( R ) ]{ 
         diff(self.S,t) = (- beta * self.S * first(I).size / N);
      }
      ...
   }   
```

This will take all equations in list of agents I and the first agent R, to make a complete system of equations.

### action

#### solve
solve all equations which matched the name, in list of agent with given method and step. there are 3 optional variable could be declared inside
  * **method**: string, mandatory, method of integration : "rk4" (only one, for instant).
  * **step**: float, mandatory, step of integration.
  * **t0**: float, optional, time initial of integration, default value: cycle-cycle\_length.
  * **tf**: float, optional, time final, default value: cycle.
  * **cycle\_length**: float, optional, length of simulation's cycle .

```
   solve SIR method: "rk4" step:0.001{ 
      float cycle_length<-1.0;
      float t0<-cycle-cycle_length;
      float tf<-cycle;    	
   }
```




## Classical Equations

A set of classical ODEs is also provided (e.g. SIR, SI... ).

### Model examples
Please find some toy models which are defined in the folder models of this plugin on SVN.