Using SavedAgent kind of GamlAgent, it is now possible to serialize and unserialize agents and simulations as a string. It can be done using the operators: `serializeSimulation`, `unserializeSimulation`, `saveSimulation` of `ummisco.gama.serialize`.

Need to be improved:
* serialization of random generator
* serialization of shapes
* to allow any agent to be serialized


Example of use of the two operators:
```
experiment toto {
	list<string> history <- [];

	reflex store when: (cycle < 6){
		add serializeSimulation(cycle) to: history;
	}
	
	reflex restore when: (cycle = 6){
		int i <- unSerializeSimulation(string(history[0]));
	} 
	
	reflex store22 when: cycle=2{
		write "Sauvegarde de la simulation " + saveSimulation("file.xml");
	}
}
```
