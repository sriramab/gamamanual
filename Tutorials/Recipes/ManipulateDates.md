# Manipulate Dates

[//]: # (keyword|type_date) 
[//]: # (keyword|concept_time)
## Managing Time in Models

If some models are based on a abstract time - only the number of cycles is important - others are based on a real time. In order to manage the time, GAMA provides some tools to manage time.

First, GAMA allows to define the duration of a simulation step. It provides access to different time variables. At last, since GAMA 1.7, it provides a date variable type and some global variables allowing to use a real calendar to manage time.

## Definition of the step and use of temporal unity values
GAMA provides three important global variables to manage time (https://github.com/gama-platform/gama/wiki/G__GlobalSpecies#cycle):
* cycle (int - not modifiable): the current simulation step - this variable is incremented by 1 at each simulation step
* step (float - can be modified): the duration of a simulation step (in seconds). By default the duration is one second.
* time (float - not modifiable): the current time spent since the beginning of the simulation - this variable is computed at each simulation step by: time = cycle * step. 

The value of the cycle and time variables are shown in the top left (green rectangle) of the simulation interface. Clicking on the green rectangle allows to display either the number cycles or the time variable. Concerning this variable, it is presented following a years - month - days - hours - minutes - seconds format. In this presentation, every months are considered as being composed of 30 days (the different number of days of months are not taken into account).

Concerning the step facet, the variable can be modified by the modeler. A classic way of doing it consists in reediting the variable in the global section:

`
global {
       float step <- 1 #hour;
}
`
In this example, each simulation step will represent 1 hour. This time will be taken into account for all actions based on time (e.g. moving actions).

Note that the value of the step variable should be given in seconds. To facilitate the definition of the step value and of all expressions based on time, GAMA provides different built-in constant variables accessible with the "#" symbol (https://github.com/gama-platform/gama/wiki/G__UnitsAndConstants#time-units): 
 * #s : second - 1 second
 * #mn : minute - 60 seconds
 * #hour : hour - 60 minutes - 3600 seconds
 * #day : day - 24 hours - 86400 seconds
 * #month : month - 30 days - 2592000 seconds
 * #year : year - 12 month - 3.1104E7
	

## The date variable type and the use of a real calendar
//definition of the date of begining of the simulation - defining this date will allows to change the normal date management of the simulation by a more realistic one (using calendar) 
	date starting_date <- date([2011,1,2,1,1,30]);
	
	//be careful, when real dates are used, modelers should not use the #month and #year values that are not consistent with them
	float step <- 1#h;
		
	init {
		write "starting_date: " + starting_date;
		
		//there are several ways to define a date.
		//The simplest consists in using a list of int values: [year,month of the year,day of the month, hour of the day, minute of the hour, second of the minute]
		date my_date <- date([2010,3,23,17,30,10]); //correspond the 23th of March 2010, at 17:30:10
		
		//It is also possible to define a date through a string:
		date my_date2 <- date("2010-3-23T17:30:10+07:00"); 
		write (my_date2);
	
		//it is possible to get the current date by using the "now" string:
		date today <- date("now"); 
		write (today);
		
		write "\n ----------------------------------------------- " ;
		
		//GAMA provides several operator to manipulate dates:	
			
		//for instance, it is possible to compute the duration in seconds between 2 dates:
		float d <- starting_date - my_date;
		write "duration between " + my_date + " and " + starting_date + " : " + d + "s";
		
		write "\n ----------------------------------------------- " ;
		
		//to add or substract a duration (in secondes) to a date:
		 write "my_date2 + 10: " + (my_date2 + 10);
		 write "my_date2 - 10: " + (my_date2 - 10);
		 
		 write "\n ----------------------------------------------- " ;
		 
		 
		 //to add or substract a duration (in years, months, weeks, days, hours, minutes,  secondes) to a date:
		  write "my_date2 add_years 1: " + (my_date2 add_years 1);
		  write "my_date2 add_months 1: " + (my_date2 add_months 1);
		  write "my_date2 add_weeks 1: " + (my_date2 add_weeks 1);
		  write "my_date2 add_days 1: " + (my_date2 add_days 1);
		  write "my_date2 add_hours 1: " + (my_date2 add_hours 1);
		  write "my_date2 add_minutes 1: " + (my_date2 add_minutes 1);
		  write "my_date2 add_seconds 1: " + (my_date2 add_seconds 1);
		  
		  write "my_date2 substract_years 1: " + (my_date2 substract_years 1);
		  write "my_date2 substract_months 1: " + (my_date2 substract_months 1);
		  write "my_date2 substract_weeks 1: " + (my_date2 substract_weeks 1);
		  write "my_date2 substract_days 1: " + (my_date2 substract_days 1);
		  write "my_date2 substract_hours 1: " + (my_date2 substract_hours 1);
		  write "my_date2 substract_minutes 1: " + (my_date2 substract_minutes 1);
		  write "my_date2 substract_seconds 1: " + (my_date2 substract_seconds 1);
	}
	
	reflex info_date {
		//at each simulation step, the current_date is updated - its value can be seen in the top-left green info panel.
		write "current_date at cycle " + cycle + " : " + current_date;
	}
}

experiment main type: gui;