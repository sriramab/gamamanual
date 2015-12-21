TO FINISH 
Add references to : 
* integration method
* ODE system (LV)

# Using Equations

## Introduction

ODEs (Ordinary Differential Equations) are often used in ecology or in epidemiology to describe the macroscopic evolution over time of a population. Generally the whole population is split into several compartments. The state of the population is described by the number of individuals in each compartment. Each equation of the ODE system describes the evolution of the number of individual in a compartment. In such an approach individuals are not taken into account individually, with own features and behaviors. In contrary they are aggregated in a compartment and reduced to a number.

A classical example is the SIR epidemic model representing the spreading of a disease in a population. The population is split into 3 compartments: S (Susceptible), I (Infected), R (Recovered). (see below for the equation)

In general the ODE systems cannot be analytically solved, i.e. it is not possible to find the equation describing the evolution of the number of S, I or R. But these systems can be numerically integrated in order to get the evolution. A numerical integration computes step after step the value of S, I and R. Several integration methods exist (e.g. Euler, Runge-Kutta...), each of them being a compromise between accuracy and computation time. The length of the integration step has also a huge impact on precision. These models are deterministic.

This approach makes a lot of strong hypotheses. The model does not take into account space. The population is considered has infinite and homogeneously mixed, so that any agent can interact with any other one.

## Example of a SIR model 

In the SIR model, the population is split into 3 compartments: S (Susceptible), I (Infected), R (Recovered). This can be represented by the following Forrester diagram: boxes represent stocks (i.e. compartments) and arrows are flows. Arrows hold the rate of a compartment population flowing to another compartment.

![](images/equations/SIR-compartments.png)

The corresponding ODE system contains one equation per stock. For example, the I compartment evolution is influenced by an inner (so positive) flow from the S compartment and an outer (so negative) flow to the R compartment.

![](images/equations/SIR-equations.png)

Integrating this system using the Runge-Kutta 4 method provides the evolution of S, I and R over time. The initial values are:
* S = 499
* I = 1
* R = 0
* beta = 0.4
* gamma = 0.1 
* h = 0.1

![](images/equations/SIR-result.png)


## Why and when can we use ODE in agent-based models ?

These hypotheses are very strong and cannot be fulfilled in agent-based models. 

But in some multi-scale models, some entities can be close. For example if we want to implement a model describing the worldwide epidemic spread and the impact of air traffic on it, we cannot simulate the 7 billions people. But we can represent only cities with airports and airplanes as agents. In this case, cities are entities with a population of millions inhabitants, that will not been spatially located. As we are only interested in the disease spread, we are only interested in the number of infected people in the cities (and susceptibles and recovered too). As a consequence, it appears particularly relevant to describe the evolution of the disease in the city using a ODE system.

In addition these models have the advantage to not be sensible to population size in the integration process. Dozens or billions people does not bring a computation time increase, contrarily to agent-based models.

## Use of ODE in a GAML model

A stereotypical use of ODE in a GAMA agent-based model is to describe species where some agents attributes evolution is described using an ODE system.

As a consequence, the GAML language has been increased by two main concepts (as two statements):
* equations can be written with the ``equation`` statement. An ``equation`` block is composed of a set of ``diff`` statement describing the evolution of species attributes.
* an equation can be numerically integrated using the ``solve`` statement

## ``equation``
### Defining an ODE system
Defining a new ODE system needs to define a new ``equation`` block in a species. As example, the following eqSI system describes the evolution of a population with 2 compartments (S and I) and the flow from S to I compartment: 
``` 
species userSI {
	float t ;
	float I ; 
	float S ; 
	int N ;
	float beta<-0.4 ;
	float h ;
	
	equation eqSI {
		diff(S,t) = -beta * S * I / N ;
		diff(I,t) = beta * S * I / N ;
	}
}			
```
This equation has to be defined in a species with ``t``, ``S`` and ``I`` attributes. ``beta`` (and other similar parameter) can be defined either in the specific species (if it is specific to each agents) or in the ``global`` if it is a constant.

### Using a built-in ODE system
In order to ease the use of very classical ODE system, some built-in systems have been implemented in GAMA. For example, the previous SI system can be written as follows. Three additional facets are used to define the system:
* `type`: the identifier of the built-in system (here SI) (the list of all built-in systems are described below),
* `vars`: this facet is expecting a list of variables of the species, that will be matched with the variables of the system,
* `params`: this facet is expecting a list of variables of the species (of of the global), that will be matched with the parameters of the system.
```
equation eqBuiltInSI type: SI vars: [S,I,t] params: [N,beta] ;
```

### Split a system into several agents

An equation system can be split into several species.

## ``solve`` an equation
The `solve` statement has been added in order to numerically integrate the equation system. It should be add into a reflex. At each simulation step, a step of the integration is executed, the length of the integration step is defined in the `step` facet. The `solve` statement will update the variables used in the equation system. The chosen integration method (defined in `method`) is Runge-Kutta 4 (which is very often a good choice of integration method in terms of accuracy).
```
reflex solving {
	solve eqSI method:rk4 step:h;
}
```
With a smaller integration step, the integration will be faster but less accurate.



## More details

### Details about the `solve` statement

### Example of the influence of the integration step

### List of built-in ODE systems
Several built-in equations have been defined.
* `equation eqBuiltInSI type: SI vars: [S,I,t] params: [N,beta];`

![](images/equations/SI-compartments.png)

![](images/equations/SI-equations.png)

![](images/equations/SI-result.png)

* `equation eqSIS type: SIS vars: [S,I,t] params: [N,beta,gamma];`

![](images/equations/SIS-compartments.png)

![](images/equations/SIS-equations.png)

![](images/equations/SIS-result.png)
