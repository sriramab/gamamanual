
<br />
# <font color='blue'>Purpose</font>

This model illustrates how to load GIS data (shapefiles) and to read attributes from GIS data.

# <font color='blue'>Formulation</font>
  * Define a species Building
  * Read the 'NATURE' and 'COMPANY' attribute of the building data: the buildings of 'Residential' type will be colored in red, the buildings of 'Industrial' type will be color in blue

# <font color='blue'>Model</font>


## Entities
We define one species of agents: the **Building** agents.

We define a 3 attribute: **mycolor** of type _rgb_, **type** of type _string_, **company** of type string

We do not specify behavior yet in this model.

In this model, we want to represent the geometry of the agent, we then use the keyword **draw** that allow to draw a given geometry. When an agent has a company name we also display it as a text.


```
entities {
  species Buildings {
    string type;
    string company;
    rgb mycolor;
	
    aspect asp1 {
      draw shape color: mycolor;
      if (company != "") {
        draw "" + company at: location size: 20 color:rgb('black');
      }
    }
  }
}
```


## GIS data loading
In GAMA, the agentification of GIS data is very straightforward: it only requires to use the create command with the from facet to pass the shapefile. Each object of the shapefile will be directly used to instantiate an agent of the specified species. The reading of an attribute in a shapefile is also very simple. It only requires to use the with facet: the argument of this facet is a dictionary of which the keys are the names of the agent attributes and the value the read command followed by the name of the shapefile attribute ("NATURE" in our case).

Init section of the global block: creation of the road and building agents from the shape files. Concerning the building agents, reading of the "NATURE" attribute of the shapefile to initiate the value of the type attribute. If the type attribute is equal to "Industrial" set the color attribute to "blue", if the type attribute is equal to "Residential" set the color attribute to "red". Then redaing the attribute "COMPANY" to display the name of the Company.

```
global {
  ...
  init {
    create Buildings from: shape_file_buildings 
    with: [type::   string(read('NATURE')), company::string(read('COMPANY'))] {
      if type = 'Industrial' {
        mycolor <- rgb('blue');
      } else if type = 'Residential' {
        mycolor <- rgb('red');
      }
    }
  }
}
```


## Environment
Building a GIS environment in GAMA requires nothing special, just to define the bounds of the environment, in our case the bounds of the building shapefile will be use to define the environment.

```
global {
  file shape_file_buildings <- file('../includes/building.shp');
  geometry shape <- envelope(shape_file_buildings);
}
```

## Display
We define a display to draw agents. We use for that the classic **species** keyword.
In the **experiment** block:
```
output {
  display disp1 refresh_every: 1 {
    species Buildings aspect: asp1;
  }
}
```

# <font color='blue'>Complete model</font>

```

model model2 
 
global {
  file shape_file_buildings <- file('../includes/building.shp');
  geometry shape <- envelope(shape_file_buildings);
  
  init {
    create Buildings from: shape_file_buildings 
    with: [type::   string(read('NATURE')), company::string(read('COMPANY'))] {
      if type = 'Industrial' {
        mycolor <- rgb('blue');
      } else if type = 'Residential' {
        mycolor <- rgb('red');
      }
    }
  }
}

entities {
  species Buildings {
    string type;
    string company;
    rgb mycolor;
	
    aspect asp1 {
      draw shape color: mycolor;
      if (company != "") {
        draw "" + company at: location size: 20 color:rgb('black');
      }
    }
  }
}

experiment exp2 type: gui {
  output {
    display disp1 refresh_every: 1 {
      species Buildings aspect: asp1;
    }
  }
}
```