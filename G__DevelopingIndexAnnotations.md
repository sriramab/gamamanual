# Index of annotations



Annotations are used to link Java methods and classes to GAML language.





## @action
This annotations is used to tag a method that will be considered as an action (or primitive) in GAML.
The method must have the following signature: ```
Object methodName(IScope) throws GamaRuntimeException ``` and be contained in a class annotated with @species or @skill (or a related class, like a subclass or an interface).

This annotation contains:
  * **name** (String): _the name of the variable as it can be used in GAML_.
  * **virtual** (boolean, false by default): _if true the action is virtual, i.e. equivalent to abstract method in java_.
  * **args** (set of arg, empty by default): _the list of arguments passed to this action. Each argument is an instance of arg_.
  * **doc** (set of @doc, empty by default): _the documentation associated to the action_.





## @arg
This annotations describes an argument passed to an action.

This annotation contains:
  * **name** (String, "" by default): _the name of the argument as it can be used in GAML_.
  * **type** (set of ints, empty by default): _An array containing the textual representation of the types that can be taken by the argument (see IType)_.
  * **optional** (boolean, true by default): _whether this argument is optional or not_.
  * **doc** (set of @doc, empty by default): _the documentation associated to the argument._





## @doc
It provides a unified way of attaching documentation to the various GAML elements tagged by the other annotations. The documentation is automatically assembled at compile time and also used at runtime in GAML editors.
  * **value** (String, "" by default): _a String representing the documentation of a GAML element_.
  * **deprecated** (String, "" by default): _a String indicating (if it is not empty) that the element is deprecated and defining, if possible, what to use instead_.
  * **returns** (String, "" by default): _the documentation concerning the value(s) returned by this element (if any)._.
  * **comment** (String, "" by default): _an optional comment that will appear differently from the documentation itself_.
  * **special\_cases** (set of Strings, empty by default): _an array of String representing the documentation of the "special cases" in which the documented element takes part_.
  * **examples** (set of Strings, empty by default): _an array of String representing some examples or use-cases about how to use this element_.
  * **see** (set of Strings, empty by default): _an array of String representing cross-references to other elements in GAML_.





## @facet
This facet describes a facet in a list of facets.

This annotation contains:
  * **name** (String): _the name of the facet. Must be unique within a symbol_.
  * **type** (set of Strings): _the string values of the different types that can be taken by this facet_.
  * **values** (set of Strings): _the values that can be taken by this facet. The value of the facet expression will be chosen among the values described here_.
  * **optional** (boolean, false by default): _whether or not this facet is optional or mandatory_.
  * **doc** (set of @doc, empty by default): _the documentation associated to the facet_.





## @facets
This annotation describes a list of facets used by a statement in GAML.

This annotation contains:
  * **value** (set of @facet): array of @facet, each representing a facet name, type..
  * **ommissible** (string): _the facet that can be safely omitted by the modeler (provided its value is the first following the keyword of the statement)_.





## @getter
This annotations is used to indicate that a method is to be used as a getter for a variable defined in the class. The variable must be defined on its own (in vars).

This annotation contains:
  * **value** (String): the name of the variable for which the annotated method is to be considered as a getter.
  * **initializer** (boolean, false by default): returns whether or not this getter shoud also be used as an initializer





## @inside
This annotation is used in conjunction with symbol. Provides a way to tell where this symbol should be located in a model (i.e. what its parents should be). Either direct symbol names (in symbols) or generic symbol kinds can be used.

This annotation contains:
  * **symbols** (set of Strings, empty by default): _symbol names of the parents_.
  * **kinds** (set of int, empty by default): _generic symbol kinds of the parents (see [ISymbolKind.java](http://code.google.com/p/gama-platform/source/browse/branches/GAMA_CURRENT/msi.gama.processor/src/msi/gama/precompiler/ISymbolKind.java) for more details)_.





## @operator
This annotation represents an "operator" in GAML, and is used to define its name(s) as well as some meta-data that will be used during the validation process.

This annotation contains:
  * **value** (set of string, empty by default): _names of the operator_.
  * **content\_type** (integer) : _if the operator returns a container, type of elements contained in the container_
  * **can\_be\_const** (boolean, false by default): _if true: if the operands are constant, returns a constant value_.
  * **category** (set of string, empty by default): _categories to which the operator belong (for documentation purpose)_.
  * **doc** (set of @doc, empty by default): _the documentation attached to this operator._






## @serializer
It allows to declare a custom serializer for Symbols (statements, var declarations, species ,experiments, etc.). This serializer will be called instead of the standard serializer, superseding this last one. Serializers must be subclasses of the SymbolSerializer class.
  * **value** (Class): _the serializer class_.






## @setter
This annotations is used to indicate that a method is to be used as a setter for a variable defined in the class. The variable must be defined on its own (in vars).

This annotation contains:
  * **value** (String): the name of the variable for which the annotated method is to be considered as a setter.






## @skill
This annotations Allows to define a new skill (class grouping variables and actions that can be used by agents).

This annotation contains:
  * **name** (String): _a String representing the skill name in GAML (must be unique throughout GAML)_.
  * **attach\_to** (set of strings): _an array of species names to which the skill will be automatically added (complements the "skills" parameter of species)_.
  * **internal** (boolean, false by default): _return whether this skill is for internal use only_.
  * **doc** (set of @doc, empty by default): _the documentation associated to the skill_.





## @species
This annotation represents a "species" in GAML. The class annotated with this annotation will be the support of a species of agents.

This annotation contains:
  * **name** (string): _the name of the species that will be created with this class as base. Must be unique throughout GAML_.
  * **skills** (set of strings, empty by default): _An array of skill names that will be automatically attached to this species._ Example: ```
 @species(value="animal" skills={"moving"}) ```
  * **internal** (boolean, false by default): _whether this species is for internal use only_.
  * **doc** (set of @doc, empty by default): _the documentation attached to this operator._






## @symbol
This annotation represents a "statement" in GAML, and is used to define its name(s) as well as some meta-data that will be used during the validation process.

This annotation contains:
  * **name** (set of string, empty by default): _names of the statement_.
  * **kind** (int): _the kind of the annotated symbol (see [ISymbolKind.java](http://code.google.com/p/gama-platform/source/browse/branches/GAMA_CURRENT/msi.gama.processor/src/msi/gama/precompiler/ISymbolKind.java) for more details)_.
  * **with\_scope** (boolean, true by default): _indicates if the statement (usually a sequence) defines its own scope. Otherwise, all the temporary variables defined in it are actually defined in the super-scope_.
  * **with\_sequence** (boolean): _indicates wether or not a sequence can or should follow the symbol denoted by this class_.
  * **with\_args** (boolean, false by default): _indicates wether or not the symbol denoted by this class will accept arguments_.
  * **remote\_context** (boolean, false by default): _indicates that the context of this statement is actually an hybrid context: although it will be executed in a remote context, any temporary variables declared in the enclosing scopes should be passed on as if the statement was executed in the current context_.
  * **doc** (set of @doc, empty by default): _the documentation attached to this symbol_.





## @type
It provides information necessary to the processor to identify a type.

This annotation contains:
  * **name** (String, "" by default): _a String representing the type name in GAML_.
  * **id** (int, 0 by default): _the unique identifier for this type. User-added types can be chosen between IType.AVAILABLE\_TYPE and IType.SPECIES\_TYPE (exclusive) (cf. [IType.java](http://code.google.com/p/gama-platform/source/browse/branches/GAMA_CURRENT/msi.gama.core/src/msi/gaml/types/IType.java))_.
  * **wraps** (tab of Class, null by default): _the list of Java Classes this type is "wrapping" (i.e. representing). The first one is the one that will be used preferentially throughout GAMA. The other ones are to ensure compatibility, in operators, with compatible Java classes (for instance, List and GamaList)_.
  * **kind** (int, ISymbolKind.Variable.REGULAR by default): _the kind of Variable used to store this type. See [ISymbolKind.Variable](http://code.google.com/p/gama-platform/source/browse/branches/GAMA_CURRENT/msi.gama.processor/src/msi/gama/precompiler/ISymbolKind.java)_.
  * **internal** (boolean, false by default): _whether this type is for internal use only_.
  * **doc** (set of @doc, empty by default): _the documentation associated to the facet_.






## @validator
It allows to declare a custom validator for Symbols (statements, var declarations, species ,experiments, etc.). This validator, if declared on subclasses of Symbol, will be called after the standard validation is done. The validator must be subclass of IDescriptionValidator.
  * **value** (Class): _the validator class_.





## @var
This annotation is used to describe a single variable or field.

This annotation contains:
  * **name** (String): _the name of the variable as it can be used in GAML_.
  * **type** (int): _The textual representation of the type of the variable (see IType)_.
  * **of** (int, 0 by default): _The textual representation of the content type of the variable (see IType#defaultContentType())_.
  * **index** (int, 0 by default): _The textual representation of the index type of the variable (see IType#defaultKeyType())_.
  * **constant** (int, false by default): _returns whether or not this variable should be considered as non modifiable_.
  * **init** (String, "" by default): _the initial value of this variable as a String that will be interpreted by GAML_.
  * **depend\_on** (set of Strings, empty by default): _an array of String representing the names of the variables on which this variable depends (so that they are computed before)_.
  * **internal** (boolean, false by default): _return whether this var is for internal use only_.
  * **doc** (set of @doc, empty by default): _the documentation associated to the variable_.






## @vars
This annotation is used to describe a set of variables or fields.

This annotation contains:
  * **value** (set of @var): _an Array of var instances, each representing a variable_.