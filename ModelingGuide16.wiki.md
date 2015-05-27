## Foreword
This guide describes how to define a model so that it can be compiled and experimented in GAMA. Please use the outline on the left-side of this page to refer to specific items.

## Basic syntactic conventions
The syntax of GAML is quite simple. Writing a model pertains to defining (in one or several files ending in '.gaml') a header followed by a sequence of _statements_ that declare the species of agents that will make up the model (see [Structure of a model](Sections16.md)).

A _statement_ represents either an imperative [command](Commands16.md) or a declarative one (see, for example [the declaration of attributes and variables](Variables16.md) or [the declaration of actions](ActionGAMA16.md) or [behaviors](Behaviors16.md)) and use the general form of a keyword, followed by an _expression_, a list of facets (`facet_name:` _expression_) and, possibly, a block (a sequence of statements inside curly brackets). Statements not followed by a block must end with a ";".

Expressions, which represent the values of facets, are made up of literary constants, attributes or variables names, or [operators](Operators16.md). Every expression has a [type](Types16.md).

Finally, and besides the syntactic constraints of GAML, we encourage you (as always) to comment your model as much as you can. Comments can be supplied everywhere in a model, either as inline comments (prefixed by // … ) or block comments (surrounded by /**…**/).