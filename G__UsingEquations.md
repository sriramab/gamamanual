TO FINISH 

# Using Equations

## Introduction

ODEs (Ordinary Differential Equations) are often used in ecology or in epidemiology to describe the macroscopic evolution over time of a population. Generally the whole population is split into several compartments. The state of the population is described by the number of individuals in each compartment. Each equation of the ODE system describes the evolution of the number of individual in a compartment. In such an approach individuals are not taken into account individually, with own features and behaviors. In contrary they are aggregated in a compartment and reduced to a number.

A classical example is the SIR epidemic model representing the spreading of a disease in a population. The population is split into 3 compartments: S (Susceptible), I (Infected), R (Recovered). (see below for the equation)

In general the ODE systems cannot be analytically solved, i.e. it is not possible to find the equation describing the evolution of the number of S, I or R. But these systems can be numerically integrated in order to get the evolution. A numerical integration computes step after step the value of S, I and R. Several integration methods exist (e.g. Euler, Runge-Kutta...), each of them being a compromise between accuracy and computation time. The length of the integration step has also a huge impact on precision. These models are deterministic.

This approach makes a lot of strong hypotheses. The model does not take into account space. The population is considered has infinite and homogeneously mixed, so that any agent can interact with any other one.

## Example of a SIR model 

![](images/SIR-compartments.jpg)
TODO : Compartment, equations, result series....

## Why and when can we use ODE in agent-based models ?

These hypotheses are very strong and cannot be fulfilled in agent-based models. 

But in some multi-scale models, some entities can be close. For example if we want to implement a model describing the worldwide epidemic spread and the impact of air traffic on it, we cannot simulate the 7 billions people. But we can represent only cities with airports and airplanes as agents. In this case, cities are entities with a population of millions inhabitants, that will not been spatially located. As we are only interested in the disease spread, we are only interested in the number of infected people in the cities (and susceptibles and recovered too). As a consequence, it appears particularly relevant to describe the evolution of the disease in the city using a ODE system.

In addition these models have the advantage to not be sensible to population size in the integration process. Dozens or billions peopls does not bring a computation time increase, contrarily to agent-based models.

## Use of ODE in a GAML model

A stereotypical use of ODE in a GAMA agent-base model is to describe species where some agents attributes evolution is described using an ODE system.

As a consequence, the GAML language has been increased by two main concepts (as two statements):
* equations can be written with the ``equation`` statement. An ``equation`` block is composed of a set of ``diff`` statement describing the evolution of species attributes.
* an equation can be numerically integrated using the ``solve`` statement

## ``equation``
### Defining an ODE system
Defining a new ODE system needs to define a new ``equation`` block in a species. As example, the following eqSI system describes the evolution of a population with 2 compartments (S and I) and the flow from S to I compartment: 
``` 
equation eqSI {
	diff(S,t) = -beta * S * I / N ;
	diff(I,t) = beta * S * I / N ;
}		
```
This equation has to be defined in a species with ``t``, ``S`` and ``I`` attributes. ``beta`` (and other similar parameter) can be defined either in the specific species (if it is specific to each agents) or in the ``global`` if it is a constant.

### Using a built-in ODE system
In order to ease the use of very classical ODE system, some built-in systems have been implemented in GAMA.


## ``solve`` an equation