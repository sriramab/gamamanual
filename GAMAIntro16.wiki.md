
<br />

# What's new in GAMA 1.6

The version 1.6 improves many features of the 1.5.1 :

  * correction of bugs (in particular, freeze, memory consumption)
  * performance improvement (in particular for "big" models)
  * simplification of the GAML language
  * integration of an agent browser
  * improvement of the 3D integration (new operators, new display facet bug corrections...)
  * removing of the environment block
  * more user/simulation interaction (event statement)

# Compact syntax

  * species can be used as a shortcut to the population of their instances (they are, actually, considered as a container of agents now).
Old syntax:
```
list(my_species) collect each.name
```

Equivalent compact syntax:
```
my_species collect each.name
```

  * « let » can now be replaced by the type of the temporary variable
Old syntax:
```
let a type: int <- 100; 
```

Equivalent compact syntax:
```
int a <- 100;
```

  * the contents type of containers (facet « of ») can now be described using a Java-like syntax
Old syntax:
```
let a <- [] type: list of: int; 
```

Equivalent compact syntax:
```
 list<int> a <- [];
```

  * elements in containers can be accessed with a Java-like syntax (including files).
Old syntax:
```
my_matrix at {100,100}
my_list at 10
my_map at ‘toto’
```

Equivalent compact syntax:
```
my_matrix[100,100]
my_list[10]
my_map[‘toto’]
```

  * « set » is now optional in assignments
Old syntax:
```
set a <- [1,2,3]; 
```

Equivalent compact syntax:
```
a <- [1,2,3];
```

  * « set » can be used to assign values to elements in containers (and effectively replaces « put » for that purpose)
Old syntax:
```
put 10 in: a at: 0; 
```

Equivalent compact syntax:
```
a[0] <- 10;
```

  * elements can be added to and removed from containers using a simpler syntax (not yet completely fixed, however)
Old syntax:
```
add 10 to: my_list;
remove 10 from: my_list
```

Equivalent compact syntax:
```
my_list << 10; OR my_list ++ 10; (both work for the moment)
my_list >> 10; OR my_list -- 10;
```

Note that extra facets (for instance « at » work also with these new statements).

  * units can now be used with the symbol ° and can be chained to create compound units or conversions
```
100 °m / °sec (a speed)
100° km / °mile (conversion from kilometers to miles).
```

Note that the complete syntax of GAMA can be found in the syntax model of the library.

# From GAMA 1.5.1 to GAMA 1.6
Model written with GAMA 1.5.1 should work with GAMA 1.6.
Some diffrences exist however:
## aspect of agents
Old syntax:
```
draw shape: circle size: 2 color: rgb("red"); 
```

Equivalent 1.6 syntax:
```
draw circle(2) color: rgb("red");
```

## loops on map
A loop over a map (or its use in iterators like where and collect) loop now over its **values**. To loop over its pairs, you'll have to invoke the field called "pairs".
Old syntax:
```
loop p over: eltMap
```

Equivalent 1.6 syntax:
```
loop p over: eltMap.pairs
```

## strings as variables (for images or other references)
In Gama 1.6 a « string » parameter to « draw » is now treated as… a string, and not (by default) as a path to a file as in Gama 1.5.

It means that, you have to cast to a file the « string » you want to display or Gama will display the name of the image as text.

Old syntax:
```
draw image: mystringvar+".png";
```

Equivalent 1.6 syntax:
```
draw image: file(mystringvar+".png");
```

# Documentation
The complete documentation of GAMA 1.6 can be found here:
  * [Guide of GAMA Graphic User Interface](InterfaceGuide16.md)
  * [Complete documentation on the modeling language](ModelingGuide16.md)
  * [Presentation of the extensions of GAMA](Extensions16.md): some extensions are directly integrated in GAMA 1.6 (such as the 3D, user commands and driving skill extension), other require to install the extension (e.g. the graphical modeling plugin).
  * [Tutorials](Tutorials16.md)


A PDF offline version of the documentation is available in the Downloads section:
http://gama-platform.googlecode.com/files/docGAMAv16.pdf