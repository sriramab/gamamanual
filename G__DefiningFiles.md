# Defining Files


Saving data to a file during an experiment can be achieved in several ways, depending on the needs of the modeler. One way is provided by the ['save' statement](G__Statements#save), which can be used everywhere in a model or a species. The other way, described here, is to include a **file** (or [\*output\_file\*](G__Statements#output_file) statement in the output section.

```
  file name: "file_name" type: file_type data: data_to_write;  
```

with:
  * file\_type: text, csv or xml
  * file\_name: string
  * data\_to\_write: string

Example:
```
  file name: "results" type: text data: time + "; " + nb_preys + ";" + nb_predators refresh_every: 2;  
```

Each time step (or according to the frequency defined in the 'refresh\_every' facet of the file output), a new line will be added at the end of the file. If "rewrite: false" is defined in its facets, a new file will be created for each simulation (identified by a timestamp in its name).

Optionally, a footer and a header can also be described with the corresponding facets (of type string).
