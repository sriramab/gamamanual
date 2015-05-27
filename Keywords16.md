
<br />
# <font color='blue'>constants</font>

## nil
Represents the null value (or undefined value). It is the default value of variables of type agent, point or species when they are not initialized.

## true, false
Represent the two possible values of boolean variables or expressions. (see bool).

# <font color='blue'>experiments built-in variables</font>

Experiments built-in variables belong to experiments. They can be set by an experiment (but not by the world).

## seed
  * float, represents the seed used in the computation of random numbers. Keeping the same seed between two runs of the same model ensures that the sequence of events will remain the same, which can be useful when debugging a model. Declaring it as a parameter allows the user or an external process (batch, for instance) to modify it. This variable is declared as a parameter by default.

```
experiment exp1 type: gui {
...
     float seed <- 354 parameter: true;
...
}
```

## rng
  * string, represents the random number generator used in the computation of random numbers. This variable is declared as a parameter by default. It currently accepts 4 different values:
    * 'mersenne': represents the default generator, based on the Mersenne-Twister algorithm. Very reliable;
    * 'cellular':  is a cellular automaton based generator that should be a bit faster, but less reliable;
    * 'xor':  is another choice. Much faster than the previous ones, but with short sequences; and
    * 'java': invokes the standard Java generator.


```
experiment exp1 type: gui {
...
     string rng <- 'java';
...
}
```

## model\_path
Contains the absolute path to the folder in which the current model is located. Always terminated by a trailing file separator.

## simulation
Represents the currently running simulation (aka the current "world"), which is an instance of the model species. Its value is nil until the experiment has been initialized.

# <font color='blue'>global built-in variables</font>

Global built-in variables can be accessed (and sometimes modified) by the world agent and every other agents in the model.

## world
  * represents the sole instance of the model species (i.e. the one defined in the `global` section). It is accessible from everywhere (including experiments) and gives access to built-in or user-defined global variables and actions.

## cycle
  * integer, read-only, designates the (integer) number of executions of the simulation cycles. Note that the first cycle is the cycle with number 0.


## step
  * float,  is the length, in model time, of an interval between two cycles, in seconds. Its default value is 1 (second). Each turn, the value of time is incremented by the value of step. The definition of step must be coherent with that of the agents' variables like speed. The use of time unit is particularly relevant for its definition.

```
global {
...
    float step <- 10°h;
...
}
```

## time
  * float, read-only, represents the current simulated time in seconds (the default unit). It is time in the model time. Begins at zero. Basically, we have:   **time = cycle `*` step**  .

```
global {
...
    int nb_minutes function: { int(time / 60)};
...
}
```

## duration
  * string, read-only, represents the value that is equal to the duration **in real machine time** of the last cycle.

## total\_duration
  * string, read-only, represents the sum of duration since the beginning of the simulation.

## average\_duration
  * string, read-only, represents the average of duration since the beginning of the simulation.

## machine\_time
  * float, read-only, represents the current machine time in milliseconds.

## agents
  * list, read-only, returns a list of all the agents of the model that are considered as "active" (i.e. all the agents with behaviors, excluding the places). Note that obtaining this list can be quite time consuming, as the world has to go through all the species and get their agents before assembling the result. For instance, instead of writing something like:

```
ask agents of_species my_species {
...
}
```

one would prefer to write (which is much faster):

```
ask my_species {
...
}
```

# <font color='blue'>units</font>

Units can be used to qualify the values of numeric variables. By default, unqualified values are considered as:

  * meters for distances, lengths...
  * seconds for durations
  * cubic meters for volumes
  * kilograms for masses

So, an expression like

```
float foo <- 1;
```

will be considered as 1 meter if foo is a distance, or 1 second if it is a duration, or 1 meter/second if it is a speed. If one wants to specify the unit, it can be done very simply by adding the unit symbol (° or #) followed by an unit name after the numeric value, like:

```
float foo <- 1 °centimeter;
```
or
```
float foo <- 1 #centimeter;
```

In that case, the numeric value of foo will be automatically translated to 0.01 (meter). It is recommended to always use float as the type of the variables that might be qualified by units (otherwise, for example in the previous case, they might be truncated to 0). Several units names are allowed as qualifiers of numeric variables. Their complete list is:

## length
> meter (default), meters, m, centimeters, centimeter, cm, millimeter, millimeters, mm, decimeter, decimeter, dm, kilometer, kilometers, km, mile, miles, yard, yards, inch, inches, foot, feet, ft.

## time
> second (default), seconds, sec, s, minute, minutes, mn, hour, hours, h, day, days, d, month, months, year, years, y, millisecond, milliseconds, msec.  _Note that one month equals 30 days and one year 360 days in these units_.

## mass
> kilogram (default),kilogram, kilo, kg, ton, tons, t, gram, grams, g, ounce, ounces, oz, pound, pounds, lb, lbm.

## surface
> square\_meter (default), m2, square\_meters, square\_mile, square\_miles, sqmi, square\_foot, square\_feet, sqft.

## volume
> m3 (default), liter, liters, l, centiliter, centiliters, cl, deciliter, deciliters, dl, hectoliter, hectoliters, hl.

These represent the basic metric and US units. Composed and derived units (like velocity, acceleration, special volumes or surfaces) can be obtained by combining these units using the **and / operators. For instance:**

```
float one_kmh <- 1 °km / °h const: true;
float one_millisecond <-1 °sec / 1000;
float one_cubic_inch <- 1 °sqin * 1 °inch;
... etc ...
```

## colors
In addition to the previous units, GAML provides a direct access to the 147 named colors defined in CSS (see http://www.cssportal.com/css3-color-names/). E.g,
```
rgb my_color <- °teal;
```

## pixel unit
This unit, only available when running aspects or declaring displays, can be obtained using the same approach, but returns a dynamic value instead of a fixed one. _px_ (or _pixels_), returns the value of one pixel on the current view in terms of model units.