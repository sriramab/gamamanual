
<br />
# <font color='blue'>Purpose</font>

This model illustrates how to implement an classic epidemiology model SIR
(http://en.wikipedia.org/wiki/Compartmental_models_in_epidemiology).

# <font color='blue'>Formulation</font>
  * Create a SIR model via Multi-Agent approach

# <font color='blue'>Model</font>


## Entities
  * Creation of the species **Host**
The species Host has an attribute **my\_color** of type _rgb_ take 3 value: Green as Susceptible, Red as Infected and Yellow as Immune . An attribute **location** of type _point_ that is initialized  to location of any grid.
The species Host has a moving skills (more details here # [Movement of the people agents](RoadTraficModel3v16.md)) and can thus move on the grid to a given.

The species Host is represented by a circle, size 1 unit


```
species Host skills:[moving]  {
		bool is_susceptible <- true;
		bool is_infected <- false;
        bool is_immune <- false;
        rgb my_color <- rgb('green');
        sir_grid myPlace<- one_of (sir_grid as list);
        /* next function computes the number of neighbours of the agent */
        int ngb_number  function:{ ((self) neighbours_at (neighbours_range)) of_species Host count(each)-1};
        
             
        reflex basic_move {
        	if (!randomWalk){
        		/* random walk among neighbours */
	        	myPlace <- one_of (myPlace.neighbours) ;
	            location <- myPlace.location;  		
        	}else{
        		/* move agent to a random place anywhere in the grid */
				myPlace <- any(sir_grid);
				location <- myPlace.location;		
        	}			 
        }
 ....
 ....
 
		aspect basic {
	        draw circle(1) color: my_color; 
        }
}
```


  * Behaviours defined in species SIR, which is transition between 3 states Susceptible, Infected and Immune.

```
species Host skills:[moving]  {
...
...
        reflex become_infected when: (is_susceptible){
	        	if (flip(1 - (1 - beta)  ^ (((self) neighbours_at (neighbours_range)) of_species Host) count (each.is_infected))) {
	        		is_susceptible <-  false;
	            	is_infected <-  true;
	            	is_immune <-  false;
	            	my_color <-  rgb('red');       	
	        }
        }
        
        reflex infecte_others when: (is_infected){
          			loop hst over: ((self) neighbours_at (neighbours_range)) of_species Host{
        			if (Host(hst).is_susceptible){
        				if(flip(beta)){
			 	        	hst.is_susceptible <-  false;
				            hst.is_infected <-  true;
				            hst.is_immune <-  false;
				            hst.my_color <-  rgb('red');     		
        				}    				
        			}
        		}
        }
        
        reflex become_immune when: (is_infected) {
        	if(flip(delta)){
	        	is_susceptible <- false;
	        	is_infected <- false;
	            is_immune <- true;
	            my_color <- rgb('yellow');        		
        	}
        }
...		
    }
```





## SIR initialization
We initialze beginning status of SIR model, include number of S, I, R with global variable initial\_S, initial\_I, initial\_R. Each agent localized at random grid.
```
init {			
			create Host number: (initial_S) {				
       			location <- myPlace.location;
	        	is_susceptible <- true;
	        	is_infected <-  false;
	            is_immune <-  false; 
	            my_color <-  rgb('green');
	        }     
	        create Host number: (initial_I) {	        					
       			location <- myPlace.location;
	            is_susceptible <-  false;
	            is_infected <-  true;
	            is_immune <-  false; 
	            my_color <-  rgb('red'); 
	       }
	       create Host number: (initial_R) {				
       			location <- myPlace.location;
	            is_susceptible <-  false;
	            is_infected <-  false;
	            is_immune <-  true; 
	            my_color <-  rgb('yellow'); 			
			}  
}
```



# <font color='blue'>Complete model</font>

```
model SIR_ABM

global { 
	geometry shape<-envelope(square(50));
	
    int initial_S <- 495 parameter: 'Number of Susceptible';  // The number of susceptible
    int initial_I <- 5 parameter: 'Number of Infected';	// The number of infected
    int initial_R <- 0 parameter: 'Number of Removed';	// The number of removed 
	int number_Hosts <- initial_S+initial_I+initial_R; // Total number of individuals

	float beta <- 0.1 parameter: 'Beta (S->I)'; 	// The parameter Beta
	float delta <- 0.01 parameter: 'Delta (I->R)'; // The parameter Delta
	
	int gridSize <- 1; //size of the grid
	int neighbours_range <- 1 min:1 max: 5 parameter:'Size of the neighbours';
	float neighbourhoodSize <-1.0; // average size of the neighbourhood (in number of cells)	
	bool randomWalk <- false parameter: 'Random Walk';  // 1: agents new positions are determined according to a random walk process, 
														// new position is in the neighbourhood;
						    							// 0: agents new position is selected randomly anywhere in the grid.
	
	init {
			create Host number: (initial_S) {				
       			location <- myPlace.location;
	        	is_susceptible <- true;
	        	is_infected <-  false;
	            is_immune <-  false; 
	            my_color <-  rgb('green');
	        }     
	        create Host number: (initial_I) {	        					
       			location <- myPlace.location;
	            is_susceptible <-  false;
	            is_infected <-  true;
	            is_immune <-  false; 
	            my_color <-  rgb('red'); 
	       }
	       create Host number: (initial_R) {				
       			location <- myPlace.location;
	            is_susceptible <-  false;
	            is_infected <-  false;
	            is_immune <-  true; 
	            my_color <-  rgb('yellow'); 			
			}  
		}
  	
      
}

entities {
	
	grid sir_grid width: 50 height: 50 {
		rgb my_color <- rgb('black');
		list neighbours of: sir_grid <- (self neighbours_at neighbours_range) of_species sir_grid;       
    }

	species Host skills:[moving]  {
		bool is_susceptible <- true;
		bool is_infected <- false;
        bool is_immune <- false;
        rgb my_color <- rgb('green');
        sir_grid myPlace<- one_of (sir_grid as list);
        /* next function computes the number of neighbours of the agent */
        int ngb_number  function:{ ((self) neighbours_at (neighbours_range)) of_species Host count(each)-1};
        
             
        reflex basic_move {
        	if (!randomWalk){
        		/* random walk among neighbours */
	        	myPlace <- one_of (myPlace.neighbours) ;
	            location <- myPlace.location;  		
        	}else{
        		/* move agent to a random place anywhere in the grid */
				myPlace <- any(sir_grid);
				location <- myPlace.location;		
        	}			 
        }
        


        reflex become_infected when: (is_susceptible){
	        	if (flip(1 - (1 - beta)  ^ (((self) neighbours_at (neighbours_range)) of_species Host) count (each.is_infected))) {
	        		is_susceptible <-  false;
	            	is_infected <-  true;
	            	is_immune <-  false;
	            	my_color <-  rgb('red');       	
	        }
        }
        
        reflex infecte_others when: (is_infected){
          			loop hst over: ((self) neighbours_at (neighbours_range)) of_species Host{
        			if (Host(hst).is_susceptible){
        				if(flip(beta)){
			 	        	hst.is_susceptible <-  false;
				            hst.is_infected <-  true;
				            hst.is_immune <-  false;
				            hst.my_color <-  rgb('red');     		
        				}    				
        			}
        		}
        }
        
        reflex become_immune when: (is_infected) {
        	if(flip(delta)){
	        	is_susceptible <- false;
	        	is_infected <- false;
	            is_immune <- true;
	            my_color <- rgb('yellow');        		
        	}
        }
        
        aspect basic {
	        draw circle(1) color: my_color; 
        }
    }
    
}

experiment simulation type: gui { 
 	output { 
	    display 'sir display' {
	        grid sir_grid lines: rgb("black");
	        species Host aspect: basic;
	    }
	 
	
	    display 'Time series' refresh_every: 1 {
			chart 'Susceptible' type: series background: rgb('lightGray') style: exploded {
				data 'susceptible' value: Host count(each.is_susceptible) color: rgb('green');
				data 'infected' value: Host count(each.is_infected) color: rgb('red');
				data 'immune' value: Host count(each.is_immune) color: rgb('yellow');
			}
		
		}
	}
}

```