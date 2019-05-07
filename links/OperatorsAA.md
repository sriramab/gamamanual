# Operators (A to A)
 	


	
    	
----

[//]: # (keyword|operator_-)
### `-`

#### Possible use: 
  *  **`-`** (`int`) --->  `int`
  *  **`-`** (`point`) --->  `point`
  *  **`-`** (`float`) --->  `float`
  * `date` **`-`** `date` --->  `float`
  *  **`-`** (`date` , `date`) --->  `float`
  * `matrix` **`-`** `float` --->  `matrix`
  *  **`-`** (`matrix` , `float`) --->  `matrix`
  * `rgb` **`-`** `int` --->  `rgb`
  *  **`-`** (`rgb` , `int`) --->  `rgb`
  * `float` **`-`** `matrix` --->  `matrix`
  *  **`-`** (`float` , `matrix`) --->  `matrix`
  * `map` **`-`** `map` --->  `map`
  *  **`-`** (`map` , `map`) --->  `map`
  * `int` **`-`** `matrix` --->  `matrix`
  *  **`-`** (`int` , `matrix`) --->  `matrix`
  * `int` **`-`** `int` --->  `int`
  *  **`-`** (`int` , `int`) --->  `int`
  * `int` **`-`** `float` --->  `float`
  *  **`-`** (`int` , `float`) --->  `float`
  * `point` **`-`** `int` --->  `point`
  *  **`-`** (`point` , `int`) --->  `point`
  * `point` **`-`** `float` --->  `point`
  *  **`-`** (`point` , `float`) --->  `point`
  * `map` **`-`** `pair` --->  `map`
  *  **`-`** (`map` , `pair`) --->  `map`
  * `date` **`-`** `float` --->  `date`
  *  **`-`** (`date` , `float`) --->  `date`
  * `geometry` **`-`** `geometry` --->  `geometry`
  *  **`-`** (`geometry` , `geometry`) --->  `geometry`
  * `matrix` **`-`** `int` --->  `matrix`
  *  **`-`** (`matrix` , `int`) --->  `matrix`
  * `rgb` **`-`** `rgb` --->  `rgb`
  *  **`-`** (`rgb` , `rgb`) --->  `rgb`
  * `float` **`-`** `float` --->  `float`
  *  **`-`** (`float` , `float`) --->  `float`
  * `matrix` **`-`** `matrix` --->  `matrix`
  *  **`-`** (`matrix` , `matrix`) --->  `matrix`
  * `date` **`-`** `int` --->  `date`
  *  **`-`** (`date` , `int`) --->  `date`
  * `geometry` **`-`** `float` --->  `geometry`
  *  **`-`** (`geometry` , `float`) --->  `geometry`
  * `geometry` **`-`** `container<geometry>` --->  `geometry`
  *  **`-`** (`geometry` , `container<geometry>`) --->  `geometry`
  * `point` **`-`** `point` --->  `point`
  *  **`-`** (`point` , `point`) --->  `point`
  * `list` **`-`** `unknown` --->  `list`
  *  **`-`** (`list` , `unknown`) --->  `list`
  * `species` **`-`** `agent` --->  `list`
  *  **`-`** (`species` , `agent`) --->  `list`
  * `container` **`-`** `container` --->  `list`
  *  **`-`** (`container` , `container`) --->  `list`
  * `float` **`-`** `int` --->  `float`
  *  **`-`** (`float` , `int`) --->  `float` 

#### Result: 
Returns the difference of the two operands.
If it is used as an unary operator, it returns the opposite of the operand.  

#### Comment: 
The behavior of the operator depends on the type of the operands.

#### Special cases:     
  * if the left operand is a species and the right operand is an agent of the species, - returns a list containing all the agents of the species minus this agent    
  * if both operands are containers and the right operand is empty, - returns the left operand    
  * if both operands are dates, returns the duration in seconds between date2 and date1. To obtain a more precise duration, in milliseconds, use milliseconds_between(date1, date2) 
  
```
 
float var0 <- date('2000-01-02') - date('2000-01-01'); // var0 equals 86400
``` 

    
  * if one operand is a color and the other an integer, returns a new color resulting from the subtraction of each component of the color with the right operand 
  
```
 
rgb var1 <- rgb([255, 128, 32]) - 3; // var1 equals rgb([252,125,29])
``` 

    
  * if one operand is a matrix and the other a number (float or int), performs a normal arithmetic difference of the number with each element of the matrix (results are float if the number is a float. 
  
```
 
matrix var2 <- 3.5 - matrix([[2,5],[3,4]]); // var2 equals matrix([[1.5,-1.5],[0.5,-0.5]])
``` 

    
  * if both operands are numbers, performs a normal arithmetic difference and returns a float if one of them is a float. 
  
```
 
int var3 <- 1 - 1; // var3 equals 0
``` 

    
  * if left-hand operand is a point and the right-hand a number, returns a new point with each coordinate as the difference of the operand coordinate with this number. 
  
```
 
point var4 <- {1, 2} - 4.5; // var4 equals {-3.5, -2.5, -4.5} 
point var5 <- {1, 2} - 4; // var5 equals {-3.0,-2.0,-4.0}
``` 

    
  * if both operands are a point, a geometry or an agent, returns the geometry resulting from the difference between both geometries 
  
```
 
geometry var6 <- geom1 - geom2; // var6 equals a geometry corresponding to difference between geom1 and geom2
``` 

    
  * if both operands are colors, returns a new color resulting from the subtraction of the two operands, component by component 
  
```
 
rgb var7 <- rgb([255, 128, 32]) - rgb('red'); // var7 equals rgb([0,128,32])
``` 

    
  * if one of the operands is a date and the other a number, returns a date corresponding to the date minus the given number as duration (in seconds) 
  
```
 
date var8 <- date('2000-01-01') - 86400; // var8 equals date('1999-12-31')
``` 

    
  * if the left-hand operand is a geometry and the right-hand operand a float, returns a geometry corresponding to the left-hand operand (geometry, agent, point) reduced by the right-hand operand distance 
  
```
 
geometry var9 <- shape - 5; // var9 equals a geometry corresponding to the geometry of the agent applying the operator reduced by a distance of 5
``` 

    
  * if the right-operand is a list of points, geometries or agents, returns the geometry resulting from the difference between the left-geometry and all of the right-geometries 
  
```
 
geometry var10 <- rectangle(10,10) - [circle(2), square(2)]; // var10 equals rectangle(10,10) - (circle(2) + square(2))
``` 

    
  * if both operands are points, returns their difference (coordinates per coordinates). 
  
```
 
point var11 <- {1, 2} - {4, 5}; // var11 equals {-3.0, -3.0}
``` 

    
  * if the left operand is a list and the right operand is an object of any type (except list), - returns a list containing the elements of the left operand minus all the occurrences of this object 
  
```
 
list<int> var12 <- [1,2,3,4,5,6] - 2; // var12 equals [1,3,4,5,6] 
list<int> var13 <- [1,2,3,4,5,6] - 0; // var13 equals [1,2,3,4,5,6]
``` 

    
  * if both operands are containers, returns a new list in which all the elements of the right operand have been removed from the left one 
  
```
 
list<int> var14 <- [1,2,3,4,5,6] - [2,4,9]; // var14 equals [1,3,5,6] 
list<int> var15 <- [1,2,3,4,5,6] - [0,8]; // var15 equals [1,2,3,4,5,6]
``` 



#### Examples: 
```
 
int var16 <- - (-56); // var16 equals 56 
map var17 <- ['a'::1,'b'::2] - ['b'::2]; // var17 equals ['a'::1] 
map var18 <- ['a'::1,'b'::2] - ['b'::2,'c'::3]; // var18 equals ['a'::1] 
point var19 <- -{3.0,5.0}; // var19 equals {-3.0,-5.0} 
point var20 <- -{1.0,6.0,7.0}; // var20 equals {-1.0,-6.0,-7.0} 
map var21 <- ['a'::1,'b'::2] - ('b'::2); // var21 equals ['a'::1] 
map var22 <- ['a'::1,'b'::2] - ('c'::3); // var22 equals ['a'::1,'b'::2] 
float var23 <- 1.0 - 1; // var23 equals 0.0 
float var24 <- 3.7 - 1.2; // var24 equals 2.5 
float var25 <- 3 - 1.2; // var25 equals 1.8

```
      


#### See also: 

[milliseconds_between](operators-i-to-m#milliseconds_between), [-](operators-a-to-a#-), [+](operators-a-to-a#+), [*](operators-a-to-a#*), [/](operators-a-to-a#/), 
    	
----

[//]: # (keyword|operator_:)
### `:`

#### Possible use: 
  * `unknown` **`:`** `unknown` --->  `unknown`
  *  **`:`** (`unknown` , `unknown`) --->  `unknown`    


#### See also: 

[?](operators-a-to-a#?), 
    	
----

[//]: # (keyword|operator_::)
### `::`

#### Possible use: 
  * `any expression` **`::`** `any expression` --->  `pair`
  *  **`::`** (`any expression` , `any expression`) --->  `pair` 

#### Result: 
produces a new pair combining the left and the right operands

#### Special cases:     
  * nil is not acceptable as a key (although it is as a value). If such a case happens, :: will throw an appropriate error
    	
----

[//]: # (keyword|operator_!)
### `!`

#### Possible use: 
  *  **`!`** (`bool`) --->  `bool` 

#### Result: 
opposite boolean value.

#### Special cases:     
  * if the parameter is not boolean, it is casted to a boolean value.

#### Examples: 
```
 
bool var0 <- ! (true); // var0 equals false

```
      


#### See also: 

[bool](operators-b-to-c#bool), [and](operators-a-to-a#and), [or](operators-n-to-r#or), 
    	
----

[//]: # (keyword|operator_!=)
### `!=`

#### Possible use: 
  * `unknown` **`!=`** `unknown` --->  `bool`
  *  **`!=`** (`unknown` , `unknown`) --->  `bool`
  * `float` **`!=`** `int` --->  `bool`
  *  **`!=`** (`float` , `int`) --->  `bool`
  * `int` **`!=`** `float` --->  `bool`
  *  **`!=`** (`int` , `float`) --->  `bool`
  * `float` **`!=`** `float` --->  `bool`
  *  **`!=`** (`float` , `float`) --->  `bool`
  * `date` **`!=`** `date` --->  `bool`
  *  **`!=`** (`date` , `date`) --->  `bool` 

#### Result: 
true if both operands are different, false otherwise

#### Examples: 
```
 
bool var0 <- [2,3] != [2,3]; // var0 equals false 
bool var1 <- [2,4] != [2,3]; // var1 equals true 
bool var2 <- 3.0 != 3; // var2 equals false 
bool var3 <- 4.7 != 4; // var3 equals true 
bool var4 <- 3 != 3.0; // var4 equals false 
bool var5 <- 4 != 4.7; // var5 equals true 
bool var6 <- 3.0 != 3.0; // var6 equals false 
bool var7 <- 4.0 != 4.7; // var7 equals true 
bool var8 <- #now != #now minus_hours 1; // var8 equals true

```
      


#### See also: 

[=](operators-a-to-a#=), [>](operators-a-to-a#>), [<](operators-a-to-a#<), [>=](operators-a-to-a#>=), [<=](operators-a-to-a#<=), 
    	
----

[//]: # (keyword|operator_?)
### `?`

#### Possible use: 
  * `bool` **`?`** `any expression` --->  `unknown`
  *  **`?`** (`bool` , `any expression`) --->  `unknown` 

#### Result: 
It is used in combination with the : operator: if the left-hand operand evaluates to true, returns the value of the left-hand operand of the :, otherwise that of the right-hand operand of the :  

#### Comment: 
These functional tests can be combined together.

#### Examples: 
```
 
list<string> var0 <- [10, 19, 43, 12, 7, 22] collect ((each > 20) ? 'above' : 'below'); // var0 equals ['below', 'below', 'above', 'below', 'below', 'above']rgb col <- (flip(0.3) ? #red : (flip(0.9) ? #blue : #green)); 

```
      


#### See also: 

[:](operators-a-to-a#:), 
    	
----

[//]: # (keyword|operator_/)
### `/`

#### Possible use: 
  * `float` **`/`** `int` --->  `float`
  *  **`/`** (`float` , `int`) --->  `float`
  * `point` **`/`** `float` --->  `point`
  *  **`/`** (`point` , `float`) --->  `point`
  * `float` **`/`** `float` --->  `float`
  *  **`/`** (`float` , `float`) --->  `float`
  * `int` **`/`** `float` --->  `float`
  *  **`/`** (`int` , `float`) --->  `float`
  * `matrix` **`/`** `float` --->  `matrix`
  *  **`/`** (`matrix` , `float`) --->  `matrix`
  * `rgb` **`/`** `int` --->  `rgb`
  *  **`/`** (`rgb` , `int`) --->  `rgb`
  * `matrix` **`/`** `int` --->  `matrix`
  *  **`/`** (`matrix` , `int`) --->  `matrix`
  * `matrix` **`/`** `matrix` --->  `matrix`
  *  **`/`** (`matrix` , `matrix`) --->  `matrix`
  * `rgb` **`/`** `float` --->  `rgb`
  *  **`/`** (`rgb` , `float`) --->  `rgb`
  * `point` **`/`** `int` --->  `point`
  *  **`/`** (`point` , `int`) --->  `point`
  * `int` **`/`** `int` --->  `float`
  *  **`/`** (`int` , `int`) --->  `float` 

#### Result: 
Returns the division of the two operands.

#### Special cases:     
  * if the right-hand operand is equal to zero, raises a "Division by zero" exception    
  * if the left operand is a point, returns a new point with coordinates divided by the right operand 
  
```
 
point var0 <- {5, 7.5} / 2.5; // var0 equals {2, 3} 
point var1 <- {2,5} / 4; // var1 equals {0.5,1.25}
``` 

    
  * if one operand is a color and the other an integer, returns a new color resulting from the division of each component of the color by the right operand 
  
```
 
rgb var2 <- rgb([255, 128, 32]) / 2; // var2 equals rgb([127,64,16])
``` 

    
  * if one operand is a color and the other a double, returns a new color resulting from the division of each component of the color by the right operand. The result on each component is then truncated. 
  
```
 
rgb var3 <- rgb([255, 128, 32]) / 2.5; // var3 equals rgb([102,51,13])
``` 

    
  * if both operands are numbers (float or int), performs a normal arithmetic division and returns a float. 
  
```
 
float var4 <- 3 / 5.0; // var4 equals 0.6
``` 

    


#### See also: 

[*](operators-a-to-a#*), [+](operators-a-to-a#+), [-](operators-a-to-a#-), 
    	
----

[//]: # (keyword|operator_.)
### `.`

#### Possible use: 
  * `matrix` **`.`** `matrix` --->  `matrix`
  *  **`.`** (`matrix` , `matrix`) --->  `matrix`
  * `agent` **`.`** `any expression` --->  `unknown`
  *  **`.`** (`agent` , `any expression`) --->  `unknown` 

#### Result: 
It has two different uses: it can be the dot product between 2 matrices or return an evaluation of the expression (right-hand operand) in the scope the given agent.

#### Special cases:     
  * if the agent is nil or dead, throws an exception    
  * if both operands are matrix, returns the dot product of them 
  
```
 
matrix var0 <- matrix([[1,1],[1,2]]) . matrix([[1,1],[1,2]]); // var0 equals matrix([[2,3],[3,5]])
``` 

    
  * if the left operand is an agent, it evaluates of the expression (right-hand operand) in the scope the given agent 
  
```
 
unknown var1 <- agent1.location; // var1 equals the location of the agent agent1
``` 


    	
----

[//]: # (keyword|operator_^)
### `^`

#### Possible use: 
  * `int` **`^`** `float` --->  `float`
  *  **`^`** (`int` , `float`) --->  `float`
  * `int` **`^`** `int` --->  `float`
  *  **`^`** (`int` , `int`) --->  `float`
  * `float` **`^`** `int` --->  `float`
  *  **`^`** (`float` , `int`) --->  `float`
  * `float` **`^`** `float` --->  `float`
  *  **`^`** (`float` , `float`) --->  `float` 

#### Result: 
Returns the value (always a float) of the left operand raised to the power of the right operand.

#### Special cases:     
  * if the right-hand operand is equal to 0, returns 1    
  * if it is equal to 1, returns the left-hand operand.    
  * Various examples of power 
  
```
 
float var0 <- 2 ^ 3; // var0 equals 8.0
``` 



#### Examples: 
```
 
float var1 <- 4.84 ^ 0.5; // var1 equals 2.2

```
      


#### See also: 

[*](operators-a-to-a#*), [sqrt](operators-s-to-z#sqrt), 
    	
----

[//]: # (keyword|operator_@)
### `@`
   Same signification as [at](operators-a-to-a#at)
    	
----

[//]: # (keyword|operator_*)
### `*`

#### Possible use: 
  * `float` **`*`** `float` --->  `float`
  *  **`*`** (`float` , `float`) --->  `float`
  * `int` **`*`** `int` --->  `int`
  *  **`*`** (`int` , `int`) --->  `int`
  * `int` **`*`** `matrix` --->  `matrix`
  *  **`*`** (`int` , `matrix`) --->  `matrix`
  * `rgb` **`*`** `int` --->  `rgb`
  *  **`*`** (`rgb` , `int`) --->  `rgb`
  * `point` **`*`** `point` --->  `float`
  *  **`*`** (`point` , `point`) --->  `float`
  * `matrix` **`*`** `int` --->  `matrix`
  *  **`*`** (`matrix` , `int`) --->  `matrix`
  * `geometry` **`*`** `float` --->  `geometry`
  *  **`*`** (`geometry` , `float`) --->  `geometry`
  * `float` **`*`** `int` --->  `float`
  *  **`*`** (`float` , `int`) --->  `float`
  * `matrix` **`*`** `float` --->  `matrix`
  *  **`*`** (`matrix` , `float`) --->  `matrix`
  * `point` **`*`** `float` --->  `point`
  *  **`*`** (`point` , `float`) --->  `point`
  * `float` **`*`** `matrix` --->  `matrix`
  *  **`*`** (`float` , `matrix`) --->  `matrix`
  * `point` **`*`** `int` --->  `point`
  *  **`*`** (`point` , `int`) --->  `point`
  * `int` **`*`** `float` --->  `float`
  *  **`*`** (`int` , `float`) --->  `float`
  * `geometry` **`*`** `point` --->  `geometry`
  *  **`*`** (`geometry` , `point`) --->  `geometry`
  * `matrix` **`*`** `matrix` --->  `matrix`
  *  **`*`** (`matrix` , `matrix`) --->  `matrix` 

#### Result: 
Returns the product of the two operands.

#### Special cases:     
  * if both operands are numbers (float or int), performs a normal arithmetic product and returns a float if one of them is a float. 
  
```
 
int var1 <- 1 * 1; // var1 equals 1
``` 

    
  * if one operand is a matrix and the other a number (float or int), performs a normal arithmetic product of the number with each element of the matrix (results are float if the number is a float. 
  
```
matrix<float> m <- (3.5 * matrix([[2,5],[3,4]]));	//m equals matrix([[7.0,17.5],[10.5,14]]) 
``` 

    
  * if one operand is a color and the other an integer, returns a new color resulting from the product of each component of the color with the right operand (with a maximum value at 255) 
  
```
 
rgb var3 <- rgb([255, 128, 32]) * 2; // var3 equals rgb([255,255,64])
``` 

    
  * if both operands are points, returns their scalar product 
  
```
 
float var4 <- {2,5} * {4.5, 5}; // var4 equals 34.0
``` 

    
  * if the left-hand operand is a geometry and the right-hand operand a float, returns a geometry corresponding to the left-hand operand (geometry, agent, point) scaled by the right-hand operand coefficient 
  
```
 
geometry var5 <- circle(10) * 2; // var5 equals circle(20) 
geometry var6 <- (circle(10) * 2).location with_precision 9; // var6 equals (circle(20)).location with_precision 9 
float var7 <- (circle(10) * 2).height with_precision 9; // var7 equals (circle(20)).height with_precision 9
``` 

    
  * if the left-hand operator is a point and the right-hand a number, returns a point with coordinates multiplied by the number 
  
```
 
point var8 <- {2,5} * 4; // var8 equals {8.0, 20.0} 
point var9 <- {2, 4} * 2.5; // var9 equals {5.0, 10.0}
``` 

    
  * if the left-hand operand is a geometry and the right-hand operand a point, returns a geometry corresponding to the left-hand operand (geometry, agent, point) scaled by the right-hand operand coefficients in the 3 dimensions 
  
```
 
geometry var10 <- shape * {0.5,0.5,2}; // var10 equals a geometry corresponding to the geometry of the agent applying the operator scaled by a coefficient of 0.5 in x, 0.5 in y and 2 in z
``` 



#### Examples: 
```
 
float var0 <- 2.5 * 2; // var0 equals 5.0

```
      


#### See also: 

[/](operators-a-to-a#/), [+](operators-a-to-a#+), [-](operators-a-to-a#-), 
    	
----

[//]: # (keyword|operator_+)
### `+`

#### Possible use: 
  * `rgb` **`+`** `int` --->  `rgb`
  *  **`+`** (`rgb` , `int`) --->  `rgb`
  * `float` **`+`** `int` --->  `float`
  *  **`+`** (`float` , `int`) --->  `float`
  * `point` **`+`** `int` --->  `point`
  *  **`+`** (`point` , `int`) --->  `point`
  * `point` **`+`** `point` --->  `point`
  *  **`+`** (`point` , `point`) --->  `point`
  * `date` **`+`** `float` --->  `date`
  *  **`+`** (`date` , `float`) --->  `date`
  * `container` **`+`** `unknown` --->  `list`
  *  **`+`** (`container` , `unknown`) --->  `list`
  * `string` **`+`** `string` --->  `string`
  *  **`+`** (`string` , `string`) --->  `string`
  * `geometry` **`+`** `geometry` --->  `geometry`
  *  **`+`** (`geometry` , `geometry`) --->  `geometry`
  * `point` **`+`** `float` --->  `point`
  *  **`+`** (`point` , `float`) --->  `point`
  * `int` **`+`** `int` --->  `int`
  *  **`+`** (`int` , `int`) --->  `int`
  * `float` **`+`** `float` --->  `float`
  *  **`+`** (`float` , `float`) --->  `float`
  * `date` **`+`** `int` --->  `date`
  *  **`+`** (`date` , `int`) --->  `date`
  * `float` **`+`** `matrix` --->  `matrix`
  *  **`+`** (`float` , `matrix`) --->  `matrix`
  * `matrix` **`+`** `int` --->  `matrix`
  *  **`+`** (`matrix` , `int`) --->  `matrix`
  * `int` **`+`** `matrix` --->  `matrix`
  *  **`+`** (`int` , `matrix`) --->  `matrix`
  * `geometry` **`+`** `float` --->  `geometry`
  *  **`+`** (`geometry` , `float`) --->  `geometry`
  * `string` **`+`** `unknown` --->  `string`
  *  **`+`** (`string` , `unknown`) --->  `string`
  * `map` **`+`** `pair` --->  `map`
  *  **`+`** (`map` , `pair`) --->  `map`
  * `date` **`+`** `string` --->  `string`
  *  **`+`** (`date` , `string`) --->  `string`
  * `int` **`+`** `float` --->  `float`
  *  **`+`** (`int` , `float`) --->  `float`
  * `matrix` **`+`** `matrix` --->  `matrix`
  *  **`+`** (`matrix` , `matrix`) --->  `matrix`
  * `container` **`+`** `container` --->  `container`
  *  **`+`** (`container` , `container`) --->  `container`
  * `rgb` **`+`** `rgb` --->  `rgb`
  *  **`+`** (`rgb` , `rgb`) --->  `rgb`
  * `map` **`+`** `map` --->  `map`
  *  **`+`** (`map` , `map`) --->  `map`
  * `matrix` **`+`** `float` --->  `matrix`
  *  **`+`** (`matrix` , `float`) --->  `matrix`
  *  **`+`** (`geometry`, `float`, `int`) --->  `geometry`
  *  **`+`** (`geometry`, `float`, `int`, `int`) --->  `geometry` 

#### Result: 
Returns the sum, union or concatenation of the two operands.

#### Special cases:     
  * if one of the operands is nil, + throws an error    
  * if both operands are species, returns a special type of list called meta-population    
  * if one operand is a color and the other an integer, returns a new color resulting from the sum of each component of the color with the right operand 
  
```
 
rgb var0 <- rgb([255, 128, 32]) + 3; // var0 equals rgb([255,131,35])
``` 

    
  * if both operands are points, returns their sum. 
  
```
 
point var1 <- {1, 2} + {4, 5}; // var1 equals {5.0, 7.0}
``` 

    
  * if the right operand is an object of any type (except a container), + returns a list of the elements of the left operand, to which this object has been added 
  
```
 
list<int> var2 <- [1,2,3,4,5,6] + 2; // var2 equals [1,2,3,4,5,6,2] 
list<int> var3 <- [1,2,3,4,5,6] + 0; // var3 equals [1,2,3,4,5,6,0]
``` 

    
  * if the right-operand is a point, a geometry or an agent, returns the geometry resulting from the union between both geometries 
  
```
 
geometry var4 <- geom1 + geom2; // var4 equals a geometry corresponding to union between geom1 and geom2
``` 

    
  * if the left-hand operand is a point and the right-hand a number, returns a new point with each coordinate as the sum of the operand coordinate with this number. 
  
```
 
point var5 <- {1, 2} + 4; // var5 equals {5.0, 6.0,4.0} 
point var6 <- {1, 2} + 4.5; // var6 equals {5.5, 6.5,4.5}
``` 

    
  * if both operands are numbers (float or int), performs a normal arithmetic sum and returns a float if one of them is a float. 
  
```
 
int var7 <- 1 + 1; // var7 equals 2
``` 

    
  * if one of the operands is a date and the other a number, returns a date corresponding to the date plus the given number as duration (in seconds) 
  
```
 
date var8 <- date('2000-01-01') + 86400; // var8 equals date('2000-01-02')
``` 

    
  * if one operand is a matrix and the other a number (float or int), performs a normal arithmetic sum of the number with each element of the matrix (results are float if the number is a float. 
  
```
 
matrix var9 <- 3.5 + matrix([[2,5],[3,4]]); // var9 equals matrix([[5.5,8.5],[6.5,7.5]])
``` 

    
  * if the left-hand operand is a geometry and the right-hand operand a float, returns a geometry corresponding to the left-hand operand (geometry, agent, point) enlarged by the right-hand operand distance. The number of segments used by default is 8 and the end cap style is #round 
  
```
 
geometry var10 <- circle(5) + 5; // var10 equals circle(10)
``` 

    
  * if the left-hand operand is a string, returns the concatenation of the two operands (the left-hand one beind casted into a string) 
  
```
 
string var11 <- "hello " + 12; // var11 equals "hello 12"
``` 

    
  * if both operands are list, +returns the concatenation of both lists. 
  
```
 
list<int> var12 <- [1,2,3,4,5,6] + [2,4,9]; // var12 equals [1,2,3,4,5,6,2,4,9] 
list<int> var13 <- [1,2,3,4,5,6] + [0,8]; // var13 equals [1,2,3,4,5,6,0,8]
``` 

    
  * if both operands are colors, returns a new color resulting from the sum of the two operands, component by component 
  
```
 
rgb var14 <- rgb([255, 128, 32]) + rgb('red'); // var14 equals rgb([255,128,32])
``` 

    
  * if the left-hand operand is a geometry and the right-hand operands a float, an integer and one of #round, #square or #flat, returns a geometry corresponding to the left-hand operand (geometry, agent, point) enlarged by the first right-hand operand (distance), using a number of segments equal to the second right-hand operand and a flat, square or round end cap style 
  
```
 
geometry var15 <- circle(5) + (5,32,#round); // var15 equals circle(10)
``` 

    
  * if the left-hand operand is a geometry and the right-hand operands a float and an integer, returns a geometry corresponding to the left-hand operand (geometry, agent, point) enlarged by the first right-hand operand (distance), using a number of segments equal to the second right-hand operand 
  
```
 
geometry var16 <- circle(5) + (5,32); // var16 equals circle(10)
``` 



#### Examples: 
```
 
float var17 <- 1.0 + 1; // var17 equals 2.0 
float var18 <- 1.0 + 2.5; // var18 equals 3.5 
map var19 <- ['a'::1,'b'::2] + ('c'::3); // var19 equals ['a'::1,'b'::2,'c'::3] 
map var20 <- ['a'::1,'b'::2] + ('c'::3); // var20 equals ['a'::1,'b'::2,'c'::3] 
map var21 <- ['a'::1,'b'::2] + ['c'::3]; // var21 equals ['a'::1,'b'::2,'c'::3] 
map var22 <- ['a'::1,'b'::2] + [5::3.0]; // var22 equals ['a'::1,'b'::2,5::3.0]

```
      


#### See also: 

[-](operators-a-to-a#-), [*](operators-a-to-a#*), [/](operators-a-to-a#/), 
    	
----

[//]: # (keyword|operator_<)
### `<`

#### Possible use: 
  * `date` **`<`** `date` --->  `bool`
  *  **`<`** (`date` , `date`) --->  `bool`
  * `float` **`<`** `int` --->  `bool`
  *  **`<`** (`float` , `int`) --->  `bool`
  * `float` **`<`** `float` --->  `bool`
  *  **`<`** (`float` , `float`) --->  `bool`
  * `int` **`<`** `int` --->  `bool`
  *  **`<`** (`int` , `int`) --->  `bool`
  * `point` **`<`** `point` --->  `bool`
  *  **`<`** (`point` , `point`) --->  `bool`
  * `int` **`<`** `float` --->  `bool`
  *  **`<`** (`int` , `float`) --->  `bool`
  * `string` **`<`** `string` --->  `bool`
  *  **`<`** (`string` , `string`) --->  `bool` 

#### Result: 
true if the left-hand operand is less than the right-hand operand, false otherwise.

#### Special cases:     
  * if one of the operands is nil, returns false    
  * if both operands are points, returns true if and only if the left component (x) of the left operand if less than or equal to x of the right one and if the right component (y) of the left operand is greater than or equal to y of the right one. 
  
```
 
bool var5 <- {5,7} < {4,6}; // var5 equals false 
bool var6 <- {5,7} < {4,8}; // var6 equals false
``` 

    
  * if both operands are String, uses a lexicographic comparison of two strings 
  
```
 
bool var7 <- 'abc' < 'aeb'; // var7 equals true
``` 



#### Examples: 
```
 
bool var0 <- #now < #now minus_hours 1; // var0 equals false 
bool var1 <- 3.5 < 7; // var1 equals true 
bool var2 <- 3.5 < 7.6; // var2 equals true 
bool var3 <- 3 < 7; // var3 equals true 
bool var4 <- 3 < 2.5; // var4 equals false

```
      


#### See also: 

[>](operators-a-to-a#>), [>=](operators-a-to-a#>=), [<=](operators-a-to-a#<=), [=](operators-a-to-a#=), [!=](operators-a-to-a#!=), 
    	
----

[//]: # (keyword|operator_<=)
### `<=`

#### Possible use: 
  * `date` **`<=`** `date` --->  `bool`
  *  **`<=`** (`date` , `date`) --->  `bool`
  * `int` **`<=`** `int` --->  `bool`
  *  **`<=`** (`int` , `int`) --->  `bool`
  * `float` **`<=`** `int` --->  `bool`
  *  **`<=`** (`float` , `int`) --->  `bool`
  * `float` **`<=`** `float` --->  `bool`
  *  **`<=`** (`float` , `float`) --->  `bool`
  * `int` **`<=`** `float` --->  `bool`
  *  **`<=`** (`int` , `float`) --->  `bool`
  * `string` **`<=`** `string` --->  `bool`
  *  **`<=`** (`string` , `string`) --->  `bool`
  * `point` **`<=`** `point` --->  `bool`
  *  **`<=`** (`point` , `point`) --->  `bool` 

#### Result: 
true if the left-hand operand is less or equal than the right-hand operand, false otherwise.

#### Special cases:     
  * if one of the operands is nil, returns false    
  * if both operands are String, uses a lexicographic comparison of two strings 
  
```
 
bool var5 <- 'abc' <= 'aeb'; // var5 equals true
``` 

    
  * if both operands are points, returns true if and only if the left component (x) of the left operand if less than or equal to x of the right one and if the right component (y) of the left operand is greater than or equal to y of the right one. 
  
```
 
bool var6 <- {5,7} <= {4,6}; // var6 equals false 
bool var7 <- {5,7} <= {4,8}; // var7 equals false
``` 



#### Examples: 
```
 
bool var0 <- #now <= #now minus_hours 1; // var0 equals false 
bool var1 <- 3 <= 7; // var1 equals true 
bool var2 <- 7.0 <= 7; // var2 equals true 
bool var3 <- 3.5 <= 3.5; // var3 equals true 
bool var4 <- 3 <= 2.5; // var4 equals false

```
      


#### See also: 

[>](operators-a-to-a#>), [<](operators-a-to-a#<), [>=](operators-a-to-a#>=), [=](operators-a-to-a#=), [!=](operators-a-to-a#!=), 
    	
----

[//]: # (keyword|operator_<>)
### `<>`
   Same signification as [!=](operators-a-to-a#!=)
    	
----

[//]: # (keyword|operator_=)
### `=`

#### Possible use: 
  * `float` **`=`** `int` --->  `bool`
  *  **`=`** (`float` , `int`) --->  `bool`
  * `int` **`=`** `int` --->  `bool`
  *  **`=`** (`int` , `int`) --->  `bool`
  * `float` **`=`** `float` --->  `bool`
  *  **`=`** (`float` , `float`) --->  `bool`
  * `unknown` **`=`** `unknown` --->  `bool`
  *  **`=`** (`unknown` , `unknown`) --->  `bool`
  * `int` **`=`** `float` --->  `bool`
  *  **`=`** (`int` , `float`) --->  `bool`
  * `date` **`=`** `date` --->  `bool`
  *  **`=`** (`date` , `date`) --->  `bool` 

#### Result: 
returns true if both operands are equal, false otherwise
returns true if both operands are equal, false otherwise

#### Special cases:     
  * if both operands are any kind of objects, returns true if they are identical (i.e., the same object) or equal (comparisons between nil values are permitted) 
  
```
 
bool var0 <- [2,3] = [2,3]; // var0 equals true
``` 



#### Examples: 
```
 
bool var1 <- 4.7 = 4; // var1 equals false 
bool var2 <- 4 = 5; // var2 equals false 
bool var3 <- 4.5 = 4.7; // var3 equals false 
bool var4 <- 3 = 3.0; // var4 equals true 
bool var5 <- 4 = 4.7; // var5 equals false 
bool var6 <- #now = #now minus_hours 1; // var6 equals false

```
      


#### See also: 

[!=](operators-a-to-a#!=), [>](operators-a-to-a#>), [<](operators-a-to-a#<), [>=](operators-a-to-a#>=), [<=](operators-a-to-a#<=), 
    	
----

[//]: # (keyword|operator_>)
### `>`

#### Possible use: 
  * `float` **`>`** `int` --->  `bool`
  *  **`>`** (`float` , `int`) --->  `bool`
  * `date` **`>`** `date` --->  `bool`
  *  **`>`** (`date` , `date`) --->  `bool`
  * `int` **`>`** `float` --->  `bool`
  *  **`>`** (`int` , `float`) --->  `bool`
  * `string` **`>`** `string` --->  `bool`
  *  **`>`** (`string` , `string`) --->  `bool`
  * `float` **`>`** `float` --->  `bool`
  *  **`>`** (`float` , `float`) --->  `bool`
  * `int` **`>`** `int` --->  `bool`
  *  **`>`** (`int` , `int`) --->  `bool`
  * `point` **`>`** `point` --->  `bool`
  *  **`>`** (`point` , `point`) --->  `bool` 

#### Result: 
true if the left-hand operand is greater than the right-hand operand, false otherwise.

#### Special cases:     
  * if one of the operands is nil, returns false    
  * if both operands are String, uses a lexicographic comparison of two strings 
  
```
 
bool var5 <- 'abc' > 'aeb'; // var5 equals false
``` 

    
  * if both operands are points, returns true if and only if the left component (x) of the left operand if greater than x of the right one and if the right component (y) of the left operand is greater than y of the right one. 
  
```
 
bool var6 <- {5,7} > {4,6}; // var6 equals true 
bool var7 <- {5,7} > {4,8}; // var7 equals false
``` 



#### Examples: 
```
 
bool var0 <- 3.5 > 7; // var0 equals false 
bool var1 <- #now > #now minus_hours 1; // var1 equals true 
bool var2 <- 3 > 2.5; // var2 equals true 
bool var3 <- 3.5 > 7.6; // var3 equals false 
bool var4 <- 3 > 7; // var4 equals false

```
      


#### See also: 

[<](operators-a-to-a#<), [>=](operators-a-to-a#>=), [<=](operators-a-to-a#<=), [=](operators-a-to-a#=), [!=](operators-a-to-a#!=), 
    	
----

[//]: # (keyword|operator_>=)
### `>=`

#### Possible use: 
  * `float` **`>=`** `int` --->  `bool`
  *  **`>=`** (`float` , `int`) --->  `bool`
  * `point` **`>=`** `point` --->  `bool`
  *  **`>=`** (`point` , `point`) --->  `bool`
  * `int` **`>=`** `float` --->  `bool`
  *  **`>=`** (`int` , `float`) --->  `bool`
  * `date` **`>=`** `date` --->  `bool`
  *  **`>=`** (`date` , `date`) --->  `bool`
  * `int` **`>=`** `int` --->  `bool`
  *  **`>=`** (`int` , `int`) --->  `bool`
  * `string` **`>=`** `string` --->  `bool`
  *  **`>=`** (`string` , `string`) --->  `bool`
  * `float` **`>=`** `float` --->  `bool`
  *  **`>=`** (`float` , `float`) --->  `bool` 

#### Result: 
true if the left-hand operand is greater or equal than the right-hand operand, false otherwise.

#### Special cases:     
  * if one of the operands is nil, returns false    
  * if both operands are points, returns true if and only if the left component (x) of the left operand if greater or equal than x of the right one and if the right component (y) of the left operand is greater than or equal to y of the right one. 
  
```
 
bool var0 <- {5,7} >= {4,6}; // var0 equals true 
bool var1 <- {5,7} >= {4,8}; // var1 equals false
``` 

    
  * if both operands are string, uses a lexicographic comparison of the two strings 
  
```
 
bool var2 <- 'abc' >= 'aeb'; // var2 equals false 
bool var3 <- 'abc' >= 'abc'; // var3 equals true
``` 



#### Examples: 
```
 
bool var4 <- 3.5 >= 7; // var4 equals false 
bool var5 <- 3 >= 2.5; // var5 equals true 
bool var6 <- #now >= #now minus_hours 1; // var6 equals true 
bool var7 <- 3 >= 7; // var7 equals false 
bool var8 <- 3.5 >= 3.5; // var8 equals true

```
      


#### See also: 

[>](operators-a-to-a#>), [<](operators-a-to-a#<), [<=](operators-a-to-a#<=), [=](operators-a-to-a#=), [!=](operators-a-to-a#!=), 
    	
----

[//]: # (keyword|operator_abs)
### `abs`

#### Possible use: 
  *  **`abs`** (`float`) --->  `float`
  *  **`abs`** (`int`) --->  `int` 

#### Result: 
Returns the absolute value of the operand (so a positive int or float depending on the type of the operand).

#### Examples: 
```
 
float var0 <- abs (200 * -1 + 0.5); // var0 equals 199.5 
int var1 <- abs (-10); // var1 equals 10 
int var2 <- abs (10); // var2 equals 10

```
  
    	
----

[//]: # (keyword|operator_accumulate)
### `accumulate`

#### Possible use: 
  * `container` **`accumulate`** `any expression` --->  `list`
  *  **`accumulate`** (`container` , `any expression`) --->  `list` 

#### Result: 
returns a new flat list, in which each element is the evaluation of the right-hand operand. If this evaluation returns a list, the elements of this result are added directly to the list returned  

#### Comment: 
accumulate is dedicated to the application of a same computation on each element of a container (and returns a list). In the right-hand operand, the keyword each can be used to represent, in turn, each of the left-hand operand elements.

#### Examples: 
```
 
list var0 <- [a1,a2,a3] accumulate (each neighbors_at 10); // var0 equals a flat list of all the neighbors of these three agents 
list<int> var1 <- [1,2,4] accumulate ([2,4]); // var1 equals [2,4,2,4,2,4] 
list<int> var2 <- [1,2,4] accumulate (each * 2); // var2 equals [2,4,8]

```
      


#### See also: 

[collect](operators-b-to-c#collect), 
    	
----

[//]: # (keyword|operator_acos)
### `acos`

#### Possible use: 
  *  **`acos`** (`int`) --->  `float`
  *  **`acos`** (`float`) --->  `float` 

#### Result: 
Returns the value (in the interval [0,180], in decimal degrees) of the arccos of the operand (which should be in [-1,1]).

#### Special cases:     
  * if the right-hand operand is outside of the [-1,1] interval, returns NaN

#### Examples: 
```
 
float var0 <- acos (0); // var0 equals 90.0

```
      


#### See also: 

[asin](operators-a-to-a#asin), [atan](operators-a-to-a#atan), [cos](operators-b-to-c#cos), 
    	
----

[//]: # (keyword|operator_action)
### `action`

#### Possible use: 
  *  **`action`** (`any`) --->  `action` 

#### Result: 
Casts the operand into the type action
    	
----

[//]: # (keyword|operator_add_3Dmodel)
### `add_3Dmodel`

#### Possible use: 
  *  **`add_3Dmodel`** (`msi.gaml.types.GamaKmlExport`, `point`, `float`, `float`, `string`) --->  `msi.gaml.types.GamaKmlExport`
  *  **`add_3Dmodel`** (`msi.gaml.types.GamaKmlExport`, `point`, `float`, `float`, `string`, `date`, `date`) --->  `msi.gaml.types.GamaKmlExport` 

#### Result: 
the kml export manager with new 3D model: take the following argument: (kml, location (point),orientation (float), scale (float), file_path (string))
the kml export manager with new 3D model: take the following argument: (kml, location (point),orientation (float), scale (float), file_path (string), begin date, end date)    


#### See also: 

[add_geometry](operators-a-to-a#add_geometry), [add_icon](operators-a-to-a#add_icon), [add_label](operators-s-to-z#add_label), 
    	
----

[//]: # (keyword|operator_add_days)
### `add_days`
   Same signification as [plus_days](operators-n-to-r#plus_days)
    	
----

[//]: # (keyword|operator_add_edge)
### `add_edge`

#### Possible use: 
  * `graph` **`add_edge`** `pair` --->  `graph`
  *  **`add_edge`** (`graph` , `pair`) --->  `graph` 

#### Result: 
add an edge between a source vertex and a target vertex (resp. the left and the right element of the pair operand)  

#### Comment: 
if the edge already exists, the graph is unchanged

#### Examples: 
```
graph <- graph add_edge (source::target); 

```
      


#### See also: 

[add_node](operators-a-to-a#add_node), [graph](operators-d-to-h#graph), 
    	
----

[//]: # (keyword|operator_add_geometry)
### `add_geometry`

#### Possible use: 
  *  **`add_geometry`** (`msi.gaml.types.GamaKmlExport`, `geometry`, `float`, `rgb`) --->  `msi.gaml.types.GamaKmlExport`
  *  **`add_geometry`** (`msi.gaml.types.GamaKmlExport`, `geometry`, `rgb`, `rgb`) --->  `msi.gaml.types.GamaKmlExport`
  *  **`add_geometry`** (`msi.gaml.types.GamaKmlExport`, `geometry`, `float`, `rgb`, `rgb`) --->  `msi.gaml.types.GamaKmlExport`
  *  **`add_geometry`** (`msi.gaml.types.GamaKmlExport`, `geometry`, `float`, `rgb`, `rgb`, `date`) --->  `msi.gaml.types.GamaKmlExport`
  *  **`add_geometry`** (`msi.gaml.types.GamaKmlExport`, `geometry`, `float`, `rgb`, `rgb`, `date`, `date`) --->  `msi.gaml.types.GamaKmlExport` 

#### Result: 
the kml export manager with new geometry: take the following argument: (kml, geometry,linewidth, linecolor,fillcolor, end date)
the kml export manager with new geometry: take the following argument: (kml, geometry,linewidth, color)
the kml export manager with new geometry: take the following argument: (kml, geometry,linewidth, linecolor,fillcolor, begin date, end date)
the kml export manager with new geometry: take the following argument: (kml, geometry,linewidth, linecolor,fillcolor)
the kml export manager with new geometry: take the following argument: (kml, geometry, linecolor,fillcolor)    


#### See also: 

[add_3Dmodel](operators-a-to-a#add_3dmodel), [add_icon](operators-a-to-a#add_icon), [add_label](operators-s-to-z#add_label), 
    	
----

[//]: # (keyword|operator_add_hours)
### `add_hours`
   Same signification as [plus_hours](operators-n-to-r#plus_hours)
    	
----

[//]: # (keyword|operator_add_icon)
### `add_icon`

#### Possible use: 
  *  **`add_icon`** (`msi.gaml.types.GamaKmlExport`, `point`, `float`, `float`, `string`) --->  `msi.gaml.types.GamaKmlExport`
  *  **`add_icon`** (`msi.gaml.types.GamaKmlExport`, `point`, `float`, `float`, `string`, `date`, `date`) --->  `msi.gaml.types.GamaKmlExport` 

#### Result: 
the kml export manager with new icons: take the following argument: (kml, location (point),orientation (float), scale (float), file_path (string), begin date, end date)
the kml export manager with new icons: take the following argument: (kml, location (point),orientation (float), scale (float), file_path (string))    


#### See also: 

[add_geometry](operators-a-to-a#add_geometry), [add_icon](operators-a-to-a#add_icon), 
    	
----

[//]: # (keyword|operator_add_minutes)
### `add_minutes`
   Same signification as [plus_minutes](operators-n-to-r#plus_minutes)
    	
----

[//]: # (keyword|operator_add_months)
### `add_months`
   Same signification as [plus_months](operators-n-to-r#plus_months)
    	
----

[//]: # (keyword|operator_add_ms)
### `add_ms`
   Same signification as [plus_ms](operators-n-to-r#plus_ms)
    	
----

[//]: # (keyword|operator_add_node)
### `add_node`

#### Possible use: 
  * `graph` **`add_node`** `geometry` --->  `graph`
  *  **`add_node`** (`graph` , `geometry`) --->  `graph` 

#### Result: 
adds a node in a graph.

#### Examples: 
```
 
graph var0 <- graph add_node node(0) ; // var0 equals the graph with node(0)

```
      


#### See also: 

[add_edge](operators-a-to-a#add_edge), [graph](operators-d-to-h#graph), 
    	
----

[//]: # (keyword|operator_add_point)
### `add_point`

#### Possible use: 
  * `geometry` **`add_point`** `point` --->  `geometry`
  *  **`add_point`** (`geometry` , `point`) --->  `geometry` 

#### Result: 
A new geometry resulting from the addition of the right point (coordinate) to the left-hand geometry. Note that adding a point to a line or polyline will always return a closed contour. Also note that the position at which the added point will appear in the geometry is not necessarily the last one, as points are always ordered in a clockwise fashion in geometries

#### Examples: 
```
 
geometry var0 <- polygon([{10,10},{10,20},{20,20}]) add_point {20,10}; // var0 equals polygon([{10,10},{10,20},{20,20},{20,10}])

```
  
    	
----

[//]: # (keyword|operator_add_seconds)
### `add_seconds`
   Same signification as [+](operators-a-to-a#+)
    	
----

[//]: # (keyword|operator_add_weeks)
### `add_weeks`
   Same signification as [plus_weeks](operators-n-to-r#plus_weeks)
    	
----

[//]: # (keyword|operator_add_years)
### `add_years`
   Same signification as [plus_years](operators-n-to-r#plus_years)
    	
----

[//]: # (keyword|operator_adjacency)
### `adjacency`

#### Possible use: 
  *  **`adjacency`** (`graph`) --->  `matrix<float>` 

#### Result: 
adjacency matrix of the given graph.
    	
----

[//]: # (keyword|operator_after)
### `after`

#### Possible use: 
  *  **`after`** (`date`) --->  `bool`
  * `any expression` **`after`** `date` --->  `bool`
  *  **`after`** (`any expression` , `date`) --->  `bool` 

#### Result: 
Returns true if the current_date of the model is strictly after the date passed in argument. Synonym of 'current_date > argument'. Can be used in its composed form with 2 arguments to express the lower boundary for the computation of a frequency. Note that only dates strictly after this one will be tested against the frequency

#### Examples: 
```
reflex when: after(starting_date) {} 	// this reflex will always be run after the first step reflex when: false after(starting date + #10days) {} 	// This reflex will not be run after this date. Better to use 'until' or 'before' in that case every(2#days) after (starting_date + 1#day) 	// the computation will return true every two days (using the starting_date of the model as the starting point) only for the dates strictly after this starting_date + 1#day 

```
  
    	
----

[//]: # (keyword|operator_agent)
### `agent`

#### Possible use: 
  *  **`agent`** (`any`) --->  `agent` 

#### Result: 
Casts the operand into the type agent
    	
----

[//]: # (keyword|operator_agent_closest_to)
### `agent_closest_to`

#### Possible use: 
  *  **`agent_closest_to`** (`unknown`) --->  `agent` 

#### Result: 
An agent, the closest to the operand (casted as a geometry).  

#### Comment: 
the distance is computed in the topology of the calling agent (the agent in which this operator is used), with the distance algorithm specific to the topology.

#### Examples: 
```
 
agent var0 <- agent_closest_to(self); // var0 equals the closest agent to the agent applying the operator.

```
      


#### See also: 

[neighbors_at](operators-n-to-r#neighbors_at), [neighbors_of](operators-n-to-r#neighbors_of), [agents_inside](operators-a-to-a#agents_inside), [agents_overlapping](operators-a-to-a#agents_overlapping), [closest_to](operators-b-to-c#closest_to), [inside](operators-i-to-m#inside), [overlapping](operators-n-to-r#overlapping), 
    	
----

[//]: # (keyword|operator_agent_farthest_to)
### `agent_farthest_to`

#### Possible use: 
  *  **`agent_farthest_to`** (`unknown`) --->  `agent` 

#### Result: 
An agent, the farthest to the operand (casted as a geometry).  

#### Comment: 
the distance is computed in the topology of the calling agent (the agent in which this operator is used), with the distance algorithm specific to the topology.

#### Examples: 
```
 
agent var0 <- agent_farthest_to(self); // var0 equals the farthest agent to the agent applying the operator.

```
      


#### See also: 

[neighbors_at](operators-n-to-r#neighbors_at), [neighbors_of](operators-n-to-r#neighbors_of), [agents_inside](operators-a-to-a#agents_inside), [agents_overlapping](operators-a-to-a#agents_overlapping), [closest_to](operators-b-to-c#closest_to), [inside](operators-i-to-m#inside), [overlapping](operators-n-to-r#overlapping), [agent_closest_to](operators-a-to-a#agent_closest_to), [farthest_to](operators-d-to-h#farthest_to), 
    	
----

[//]: # (keyword|operator_agent_from_geometry)
### `agent_from_geometry`

#### Possible use: 
  * `path` **`agent_from_geometry`** `geometry` --->  `agent`
  *  **`agent_from_geometry`** (`path` , `geometry`) --->  `agent` 

#### Result: 
returns the agent corresponding to given geometry (right-hand operand) in the given path (left-hand operand).

#### Special cases:     
  * if the left-hand operand is nil, returns nil

#### Examples: 
```
geometry line <- one_of(path_followed.segments); road ag <- road(path_followed agent_from_geometry line); 

```
      


#### See also: 

[path](operators-n-to-r#path), 
    	
----

[//]: # (keyword|operator_agents_at_distance)
### `agents_at_distance`

#### Possible use: 
  *  **`agents_at_distance`** (`float`) --->  `list` 

#### Result: 
A list of agents situated at a distance lower than the right argument.

#### Examples: 
```
 
list var0 <- agents_at_distance(20); // var0 equals all the agents (excluding the caller) which distance to the caller is lower than 20

```
      


#### See also: 

[neighbors_at](operators-n-to-r#neighbors_at), [neighbors_of](operators-n-to-r#neighbors_of), [agent_closest_to](operators-a-to-a#agent_closest_to), [agents_inside](operators-a-to-a#agents_inside), [closest_to](operators-b-to-c#closest_to), [inside](operators-i-to-m#inside), [overlapping](operators-n-to-r#overlapping), [at_distance](operators-a-to-a#at_distance), 
    	
----

[//]: # (keyword|operator_agents_inside)
### `agents_inside`

#### Possible use: 
  *  **`agents_inside`** (`unknown`) --->  `list<agent>` 

#### Result: 
A list of agents covered by the operand (casted as a geometry).

#### Examples: 
```
 
list<agent> var0 <- agents_inside(self); // var0 equals the agents that are covered by the shape of the agent applying the operator.

```
      


#### See also: 

[agent_closest_to](operators-a-to-a#agent_closest_to), [agents_overlapping](operators-a-to-a#agents_overlapping), [closest_to](operators-b-to-c#closest_to), [inside](operators-i-to-m#inside), [overlapping](operators-n-to-r#overlapping), 
    	
----

[//]: # (keyword|operator_agents_overlapping)
### `agents_overlapping`

#### Possible use: 
  *  **`agents_overlapping`** (`unknown`) --->  `list<agent>` 

#### Result: 
A list of agents overlapping the operand (casted as a geometry).

#### Examples: 
```
 
list<agent> var0 <- agents_overlapping(self); // var0 equals the agents that overlap the shape of the agent applying the operator.

```
      


#### See also: 

[neighbors_at](operators-n-to-r#neighbors_at), [neighbors_of](operators-n-to-r#neighbors_of), [agent_closest_to](operators-a-to-a#agent_closest_to), [agents_inside](operators-a-to-a#agents_inside), [closest_to](operators-b-to-c#closest_to), [inside](operators-i-to-m#inside), [overlapping](operators-n-to-r#overlapping), [at_distance](operators-a-to-a#at_distance), 
    	
----

[//]: # (keyword|operator_all_pairs_shortest_path)
### `all_pairs_shortest_path`

#### Possible use: 
  *  **`all_pairs_shortest_path`** (`graph`) --->  `matrix<int>` 

#### Result: 
returns the successor matrix of shortest paths between all node pairs (rows: source, columns: target): a cell (i,j) will thus contains the next node in the shortest path between i and j.

#### Examples: 
```
 
matrix<int> var0 <- all_pairs_shortest_paths(my_graph); // var0 equals shortest_paths_matrix will contain all pairs of shortest paths

```
  
    	
----

[//]: # (keyword|operator_alpha_index)
### `alpha_index`

#### Possible use: 
  *  **`alpha_index`** (`graph`) --->  `float` 

#### Result: 
returns the alpha index of the graph (measure of connectivity which evaluates the number of cycles in a graph in comparison with the maximum number of cycles. The higher the alpha index, the more a network is connected: alpha = nb_cycles / (2`*`S-5) - planar graph)

#### Examples: 
```
 
float var1 <- alpha_index(graphEpidemio); // var1 equals the alpha index of the graph

```
      


#### See also: 

[beta_index](operators-b-to-c#beta_index), [gamma_index](operators-d-to-h#gamma_index), [nb_cycles](operators-n-to-r#nb_cycles), [connectivity_index](operators-b-to-c#connectivity_index), 
    	
----

[//]: # (keyword|operator_among)
### `among`

#### Possible use: 
  * `int` **`among`** `container` --->  `list`
  *  **`among`** (`int` , `container`) --->  `list` 

#### Result: 
Returns a list of length the value of the left-hand operand, containing random elements from the right-hand operand. As of GAMA 1.6, the order in which the elements are returned can be different than the order in which they appear in the right-hand container

#### Special cases:     
  * if the right-hand operand is empty, among returns a new empty list. If it is nil, it throws an error.    
  * if the left-hand operand is greater than the length of the right-hand operand, among returns the right-hand operand (converted as a list). If it is smaller or equal to zero, it returns an empty list

#### Examples: 
```
 
list<int> var0 <- 3 among [1,2,4,3,5,7,6,8]; // var0 equals [1,2,8] (for example) 
list var1 <- 3 among g2; // var1 equals [node6,node11,node7] 
list var2 <- 3 among list(node); // var2 equals [node1,node11,node4] 
list<int> var3 <- 1 among [1::2,3::4]; // var3 equals 2 or 4

```
  
    	
----

[//]: # (keyword|operator_and)
### `and`

#### Possible use: 
  * `bool` **`and`** `any expression` --->  `bool`
  *  **`and`** (`bool` , `any expression`) --->  `bool` 

#### Result: 
a bool value, equal to the logical and between the left-hand operand and the right-hand operand.  

#### Comment: 
both operands are always casted to bool before applying the operator. Thus, an expression like (1 and 0) is accepted and returns false.    


#### See also: 

[bool](operators-b-to-c#bool), [or](operators-n-to-r#or), [!](operators-a-to-a#!), 
    	
----

[//]: # (keyword|operator_and)
### `and`

#### Possible use: 
  * `predicate` **`and`** `predicate` --->  `predicate`
  *  **`and`** (`predicate` , `predicate`) --->  `predicate` 

#### Result: 
create a new predicate from two others by including them as subintentions

#### Examples: 
```
predicate1 and predicate2 

```
  
    	
----

[//]: # (keyword|operator_angle_between)
### `angle_between`

#### Possible use: 
  *  **`angle_between`** (`point`, `point`, `point`) --->  `float` 

#### Result: 
the angle between vectors P0P1 and P0P2 (P0, P1, P2 being the three point operands)

#### Examples: 
```
 
float var0 <- angle_between({5,5},{10,5},{5,10}); // var0 equals 90

```
  
    	
----

[//]: # (keyword|operator_any)
### `any`
   Same signification as [one_of](operators-n-to-r#one_of)
    	
----

[//]: # (keyword|operator_any_location_in)
### `any_location_in`

#### Possible use: 
  *  **`any_location_in`** (`geometry`) --->  `point` 

#### Result: 
A point inside (or touching) the operand-geometry.

#### Examples: 
```
 
point var0 <- any_location_in(square(5)); // var0 equals a point in the square, for example : {3,4.6}.

```
      


#### See also: 

[closest_points_with](operators-b-to-c#closest_points_with), [farthest_point_to](operators-d-to-h#farthest_point_to), [points_at](operators-n-to-r#points_at), 
    	
----

[//]: # (keyword|operator_any_point_in)
### `any_point_in`
   Same signification as [any_location_in](operators-a-to-a#any_location_in)
    	
----

[//]: # (keyword|operator_append_horizontally)
### `append_horizontally`

#### Possible use: 
  * `matrix` **`append_horizontally`** `matrix` --->  `matrix`
  *  **`append_horizontally`** (`matrix` , `matrix`) --->  `matrix`
  * `matrix` **`append_horizontally`** `matrix` --->  `matrix`
  *  **`append_horizontally`** (`matrix` , `matrix`) --->  `matrix` 

#### Result: 
A matrix resulting from the concatenation of the rows of the two given matrices. If not both numerical or both object matrices, returns the first matrix.

#### Examples: 
```
 
matrix var0 <- matrix([[1.0,2.0],[3.0,4.0]]) append_horizontally matrix([[1,2],[3,4]]); // var0 equals matrix([[1.0,2.0],[3.0,4.0],[1.0,2.0],[3.0,4.0]])

```
  
    	
----

[//]: # (keyword|operator_append_vertically)
### `append_vertically`

#### Possible use: 
  * `matrix` **`append_vertically`** `matrix` --->  `matrix`
  *  **`append_vertically`** (`matrix` , `matrix`) --->  `matrix`
  * `matrix` **`append_vertically`** `matrix` --->  `matrix`
  *  **`append_vertically`** (`matrix` , `matrix`) --->  `matrix` 

#### Result: 
A matrix resulting from the concatenation of the columns  of the two given matrices. If not both numerical or both object matrices, returns the first matrix.

#### Examples: 
```
 
matrix var0 <- matrix([[1,2],[3,4]]) append_vertically matrix([[1,2],[3,4]]); // var0 equals matrix([[1,2,1,2],[3,4,3,4]])

```
  
    	
----

[//]: # (keyword|operator_arc)
### `arc`

#### Possible use: 
  *  **`arc`** (`float`, `float`, `float`) --->  `geometry`
  *  **`arc`** (`float`, `float`, `float`, `bool`) --->  `geometry` 

#### Result: 
An arc, which radius is equal to the first operand, heading to the second and amplitude the third
An arc, which radius is equal to the first operand, heading to the second, amplitude to the third and a boolean indicating whether to return a linestring or a polygon to the fourth  

#### Comment: 
the center of the arc is by default the location of the current agent in which has been called this operator. This operator returns a polygon by default.the center of the arc is by default the location of the current agent in which has been called this operator.

#### Special cases:     
  * returns a point if the radius operand is lower or equal to 0.    
  * returns a point if the radius operand is lower or equal to 0.

#### Examples: 
```
 
geometry var0 <- arc(4,45,90); // var0 equals a geometry as an arc of radius 4, in a direction of 45Â° and an amplitude of 90Â° 
geometry var1 <- arc(4,45,90, false); // var1 equals a geometry as an arc of radius 4, in a direction of 45Â° and an amplitude of 90Â°, which only contains the points on the arc

```
      


#### See also: 

[around](operators-a-to-a#around), [cone](operators-b-to-c#cone), [line](operators-i-to-m#line), [link](operators-i-to-m#link), [norm](operators-n-to-r#norm), [point](operators-n-to-r#point), [polygon](operators-n-to-r#polygon), [polyline](operators-n-to-r#polyline), [super_ellipse](operators-s-to-z#super_ellipse), [rectangle](operators-n-to-r#rectangle), [square](operators-s-to-z#square), [circle](operators-b-to-c#circle), [ellipse](operators-d-to-h#ellipse), [triangle](operators-s-to-z#triangle), 
    	
----

[//]: # (keyword|operator_around)
### `around`

#### Possible use: 
  * `float` **`around`** `unknown` --->  `geometry`
  *  **`around`** (`float` , `unknown`) --->  `geometry` 

#### Result: 
A geometry resulting from the difference between a buffer around the right-operand casted in geometry at a distance left-operand (right-operand buffer left-operand) and the right-operand casted as geometry.

#### Special cases:     
  * returns a circle geometry of radius right-operand if the left-operand is nil

#### Examples: 
```
 
geometry var0 <- 10 around circle(5); // var0 equals the ring geometry between 5 and 10.

```
      


#### See also: 

[circle](operators-b-to-c#circle), [cone](operators-b-to-c#cone), [line](operators-i-to-m#line), [link](operators-i-to-m#link), [norm](operators-n-to-r#norm), [point](operators-n-to-r#point), [polygon](operators-n-to-r#polygon), [polyline](operators-n-to-r#polyline), [rectangle](operators-n-to-r#rectangle), [square](operators-s-to-z#square), [triangle](operators-s-to-z#triangle), 
    	
----

[//]: # (keyword|operator_as)
### `as`

#### Possible use: 
  * `unknown` **`as`** `msi.gaml.types.IType` --->  `unknown`
  *  **`as`** (`unknown` , `msi.gaml.types.IType`) --->  `unknown` 

#### Result: 
casting of the first argument into a given type  

#### Comment: 
It is equivalent to the application of the type operator on the left operand.

#### Examples: 
```
 
int var0 <- 3.5 as int; // var0 equals int(3.5)

```
  
    	
----

[//]: # (keyword|operator_as_4_grid)
### `as_4_grid`

#### Possible use: 
  * `geometry` **`as_4_grid`** `point` --->  `matrix`
  *  **`as_4_grid`** (`geometry` , `point`) --->  `matrix` 

#### Result: 
A matrix of square geometries (grid with 4-neighborhood) with dimension given by the right-hand operand ({nb_cols, nb_lines}) corresponding to the square tessellation of the left-hand operand geometry (geometry, agent)

#### Examples: 
```
 
matrix var0 <- self as_4_grid {10, 5}; // var0 equals the matrix of square geometries (grid with 4-neighborhood) with 10 columns and 5 lines corresponding to the square tessellation of the geometry of the agent applying the operator.

```
      


#### See also: 

[as_grid](operators-a-to-a#as_grid), [as_hexagonal_grid](operators-a-to-a#as_hexagonal_grid), 
    	
----

[//]: # (keyword|operator_as_distance_graph)
### `as_distance_graph`

#### Possible use: 
  * `container` **`as_distance_graph`** `map` --->  `graph`
  *  **`as_distance_graph`** (`container` , `map`) --->  `graph`
  * `container` **`as_distance_graph`** `float` --->  `graph`
  *  **`as_distance_graph`** (`container` , `float`) --->  `graph`
  *  **`as_distance_graph`** (`container`, `float`, `species`) --->  `graph` 

#### Result: 
creates a graph from a list of vertices (left-hand operand). An edge is created between each pair of vertices close enough (less than a distance, right-hand operand).  

#### Comment: 
as_distance_graph is more efficient for a list of points than as_intersection_graph.

#### Examples: 
```
list(ant) as_distance_graph 3.0 

```
      


#### See also: 

[as_intersection_graph](operators-a-to-a#as_intersection_graph), [as_edge_graph](operators-a-to-a#as_edge_graph), 
    	
----

[//]: # (keyword|operator_as_driving_graph)
### `as_driving_graph`

#### Possible use: 
  * `container` **`as_driving_graph`** `container` --->  `graph`
  *  **`as_driving_graph`** (`container` , `container`) --->  `graph` 

#### Result: 
creates a graph from the list/map of edges given as operand and connect the node to the edge

#### Examples: 
```
as_driving_graph(road,node)  --:  build a graph while using the road agents as edges and the node agents as nodes 

```
      


#### See also: 

[as_intersection_graph](operators-a-to-a#as_intersection_graph), [as_distance_graph](operators-a-to-a#as_distance_graph), [as_edge_graph](operators-a-to-a#as_edge_graph), 
    	
----

[//]: # (keyword|operator_as_edge_graph)
### `as_edge_graph`

#### Possible use: 
  *  **`as_edge_graph`** (`map`) --->  `graph`
  *  **`as_edge_graph`** (`container`) --->  `graph`
  * `container` **`as_edge_graph`** `float` --->  `graph`
  *  **`as_edge_graph`** (`container` , `float`) --->  `graph` 

#### Result: 
creates a graph from the list/map of edges given as operand

#### Special cases:     
  * if the operand is a map, the graph will be built by creating edges from pairs of the map 
  
```
 
graph var0 <- as_edge_graph([{1,5}::{12,45},{12,45}::{34,56}]); // var0 equals a graph with these three vertices and two edges
``` 

    
  * if the operand is a list and a tolerance (max distance in meters to consider that 2 points are the same node) is given, the graph will be built with elements of the list as edges and two edges will be connected by a node if the distance between their extremity (first or last points) are at distance lower or equal to the tolerance 
  
```
 
graph var1 <- as_edge_graph([line([{1,5},{12,45}]),line([{13,45},{34,56}])],1); // var1 equals a graph with two edges and three vertices
``` 

    
  * if the operand is a list, the graph will be built with elements of the list as edges 
  
```
 
graph var2 <- as_edge_graph([line([{1,5},{12,45}]),line([{12,45},{34,56}])]); // var2 equals a graph with two edges and three vertices
``` 

    


#### See also: 

[as_intersection_graph](operators-a-to-a#as_intersection_graph), [as_distance_graph](operators-a-to-a#as_distance_graph), 
    	
----

[//]: # (keyword|operator_as_grid)
### `as_grid`

#### Possible use: 
  * `geometry` **`as_grid`** `point` --->  `matrix`
  *  **`as_grid`** (`geometry` , `point`) --->  `matrix` 

#### Result: 
A matrix of square geometries (grid with 8-neighborhood) with dimension given by the right-hand operand ({nb_cols, nb_lines}) corresponding to the square tessellation of the left-hand operand geometry (geometry, agent)

#### Examples: 
```
 
matrix var0 <- self as_grid {10, 5}; // var0 equals a matrix of square geometries (grid with 8-neighborhood) with 10 columns and 5 lines corresponding to the square tessellation of the geometry of the agent applying the operator.

```
      


#### See also: 

[as_4_grid](operators-a-to-a#as_4_grid), [as_hexagonal_grid](operators-a-to-a#as_hexagonal_grid), 
    	
----

[//]: # (keyword|operator_as_hexagonal_grid)
### `as_hexagonal_grid`

#### Possible use: 
  * `geometry` **`as_hexagonal_grid`** `point` --->  `list<geometry>`
  *  **`as_hexagonal_grid`** (`geometry` , `point`) --->  `list<geometry>` 

#### Result: 
A list of geometries (hexagonal) corresponding to the hexagonal tesselation of the first operand geometry

#### Examples: 
```
 
list<geometry> var0 <- self as_hexagonal_grid {10, 5}; // var0 equals list of geometries (hexagonal) corresponding to the hexagonal tesselation of the first operand geometry

```
      


#### See also: 

[as_4_grid](operators-a-to-a#as_4_grid), [as_grid](operators-a-to-a#as_grid), 
    	
----

[//]: # (keyword|operator_as_int)
### `as_int`

#### Possible use: 
  * `string` **`as_int`** `int` --->  `int`
  *  **`as_int`** (`string` , `int`) --->  `int` 

#### Result: 
parses the string argument as a signed integer in the radix specified by the second argument.

#### Special cases:     
  * if the left operand is nil or empty, as_int returns 0    
  * if the left operand does not represent an integer in the specified radix, as_int throws an exception 

#### Examples: 
```
 
int var0 <- '20' as_int 10; // var0 equals 20 
int var1 <- '20' as_int 8; // var1 equals 16 
int var2 <- '20' as_int 16; // var2 equals 32 
int var3 <- '1F' as_int 16; // var3 equals 31 
int var4 <- 'hello' as_int 32; // var4 equals 18306744

```
      


#### See also: 

[int](operators-i-to-m#int), 
    	
----

[//]: # (keyword|operator_as_intersection_graph)
### `as_intersection_graph`

#### Possible use: 
  * `container` **`as_intersection_graph`** `float` --->  `graph`
  *  **`as_intersection_graph`** (`container` , `float`) --->  `graph` 

#### Result: 
creates a graph from a list of vertices (left-hand operand). An edge is created between each pair of vertices with an intersection (with a given tolerance).  

#### Comment: 
as_intersection_graph is more efficient for a list of geometries (but less accurate) than as_distance_graph.

#### Examples: 
```
list(ant) as_intersection_graph 0.5 

```
      


#### See also: 

[as_distance_graph](operators-a-to-a#as_distance_graph), [as_edge_graph](operators-a-to-a#as_edge_graph), 
    	
----

[//]: # (keyword|operator_as_map)
### `as_map`

#### Possible use: 
  * `container` **`as_map`** `any expression` --->  `map`
  *  **`as_map`** (`container` , `any expression`) --->  `map` 

#### Result: 
produces a new map from the evaluation of the right-hand operand for each element of the left-hand operand  

#### Comment: 
the right-hand operand should be a pair

#### Special cases:     
  * if the left-hand operand is nil, as_map throws an error.

#### Examples: 
```
 
map<int,int> var0 <- [1,2,3,4,5,6,7,8] as_map (each::(each * 2)); // var0 equals [1::2, 2::4, 3::6, 4::8, 5::10, 6::12, 7::14, 8::16] 
map<int,int> var1 <- [1::2,3::4,5::6] as_map (each::(each * 2)); // var1 equals [2::4, 4::8, 6::12] 

```
  
    	
----

[//]: # (keyword|operator_as_matrix)
### `as_matrix`

#### Possible use: 
  * `unknown` **`as_matrix`** `point` --->  `matrix`
  *  **`as_matrix`** (`unknown` , `point`) --->  `matrix` 

#### Result: 
casts the left operand into a matrix with right operand as preferred size  

#### Comment: 
This operator is very useful to cast a file containing raster data into a matrix.Note that both components of the right operand point should be positive, otherwise an exception is raised.The operator as_matrix creates a matrix of preferred size. It fills in it with elements of the left operand until the matrix is full If the size is to short, some elements will be omitted. Matrix remaining elements will be filled in by nil.

#### Special cases:     
  * if the right operand is nil, as_matrix is equivalent to the matrix operator    


#### See also: 

[matrix](operators-i-to-m#matrix), 
    	
----

[//]: # (keyword|operator_as_path)
### `as_path`

#### Possible use: 
  * `list<geometry>` **`as_path`** `graph` --->  `path`
  *  **`as_path`** (`list<geometry>` , `graph`) --->  `path` 

#### Result: 
create a graph path from the list of shape

#### Examples: 
```
 
path var0 <- [road1,road2,road3] as_path my_graph; // var0 equals a path road1->road2->road3 of my_graph

```
  
    	
----

[//]: # (keyword|operator_asin)
### `asin`

#### Possible use: 
  *  **`asin`** (`float`) --->  `float`
  *  **`asin`** (`int`) --->  `float` 

#### Result: 
the arcsin of the operand

#### Special cases:     
  * if the right-hand operand is outside of the [-1,1] interval, returns NaN

#### Examples: 
```
 
float var0 <- asin (0); // var0 equals 0.0 
float var1 <- asin (90); // var1 equals #nan

```
      


#### See also: 

[acos](operators-a-to-a#acos), [atan](operators-a-to-a#atan), [sin](operators-s-to-z#sin), 
    	
----

[//]: # (keyword|operator_at)
### `at`

#### Possible use: 
  * `container<KeyType,ValueType>` **`at`** `KeyType` --->  `ValueType`
  *  **`at`** (`container<KeyType,ValueType>` , `KeyType`) --->  `ValueType`
  * `string` **`at`** `int` --->  `string`
  *  **`at`** (`string` , `int`) --->  `string` 

#### Result: 
the element at the right operand index of the container  

#### Comment: 
The first element of the container is located at the index 0. In addition, if the user tries to get the element at an index higher or equals than the length of the container, he will get an IndexOutOfBoundException.The at operator behavior depends on the nature of the operand

#### Special cases:     
  * if it is a file, at returns the element of the file content at the index specified by the right operand    
  * if it is a population, at returns the agent at the index specified by the right operand    
  * if it is a graph and if the right operand is a node, at returns the in and out edges corresponding to that node    
  * if it is a graph and if the right operand is an edge, at returns the pair node_out::node_in of the edge    
  * if it is a graph and if the right operand is a pair node1::node2, at returns the edge from node1 to node2 in the graph    
  * if it is a list or a matrix, at returns the element at the index specified by the right operand 
  
```
 
int var0 <- [1, 2, 3] at 2; // var0 equals 3 
point var1 <- [{1,2}, {3,4}, {5,6}] at 0; // var1 equals {1.0,2.0}
``` 



#### Examples: 
```
 
string var2 <- 'abcdef' at 0; // var2 equals 'a'

```
      


#### See also: 

[contains_all](operators-b-to-c#contains_all), [contains_any](operators-b-to-c#contains_any), 
    	
----

[//]: # (keyword|operator_at_distance)
### `at_distance`

#### Possible use: 
  * `container<agent>` **`at_distance`** `float` --->  `list<geometry>`
  *  **`at_distance`** (`container<agent>` , `float`) --->  `list<geometry>` 

#### Result: 
A list of agents or geometries among the left-operand list that are located at a distance <= the right operand from the caller agent (in its topology)

#### Examples: 
```
 
list<geometry> var0 <- [ag1, ag2, ag3] at_distance 20; // var0 equals the agents of the list located at a distance <= 20 from the caller agent (in the same order).

```
      


#### See also: 

[neighbors_at](operators-n-to-r#neighbors_at), [neighbors_of](operators-n-to-r#neighbors_of), [agent_closest_to](operators-a-to-a#agent_closest_to), [agents_inside](operators-a-to-a#agents_inside), [closest_to](operators-b-to-c#closest_to), [inside](operators-i-to-m#inside), [overlapping](operators-n-to-r#overlapping), 
    	
----

[//]: # (keyword|operator_at_location)
### `at_location`

#### Possible use: 
  * `geometry` **`at_location`** `point` --->  `geometry`
  *  **`at_location`** (`geometry` , `point`) --->  `geometry` 

#### Result: 
A geometry resulting from the tran of a translation to the right-hand operand point of the left-hand operand (geometry, agent, point)

#### Examples: 
```
 
geometry var0 <- self at_location {10, 20}; // var0 equals the geometry resulting from a translation to the location {10, 20} of the left-hand geometry (or agent).

```
  
    	
----

[//]: # (keyword|operator_atan)
### `atan`

#### Possible use: 
  *  **`atan`** (`float`) --->  `float`
  *  **`atan`** (`int`) --->  `float` 

#### Result: 
Returns the value (in the interval [-90,90], in decimal degrees) of the arctan of the operand (which can be any real number).

#### Examples: 
```
 
float var0 <- atan (1); // var0 equals 45.0

```
      


#### See also: 

[acos](operators-a-to-a#acos), [asin](operators-a-to-a#asin), [tan](operators-s-to-z#tan), 
    	
----

[//]: # (keyword|operator_atan2)
### `atan2`

#### Possible use: 
  * `float` **`atan2`** `float` --->  `float`
  *  **`atan2`** (`float` , `float`) --->  `float` 

#### Result: 
the atan2 value of the two operands.  

#### Comment: 
The function atan2 is the arctangent function with two arguments. The purpose of using two arguments instead of one is to gather information on the signs of the inputs in order to return the appropriate quadrant of the computed angle, which is not possible for the single-argument arctangent function.

#### Examples: 
```
 
float var0 <- atan2 (0,0); // var0 equals 0.0

```
      


#### See also: 

[atan](operators-a-to-a#atan), [acos](operators-a-to-a#acos), [asin](operators-a-to-a#asin), 
    	
----

[//]: # (keyword|operator_attributes)
### `attributes`

#### Possible use: 
  *  **`attributes`** (`any`) --->  `attributes` 

#### Result: 
Casts the operand into the type attributes
    	
----

[//]: # (keyword|operator_auto_correlation)
### `auto_correlation`

#### Possible use: 
  * `container` **`auto_correlation`** `int` --->  `float`
  *  **`auto_correlation`** (`container` , `int`) --->  `float` 

#### Result: 
Returns the auto-correlation of a data sequence