[//]: # (startConcept|export_files)
# Defining export files

Displays are not the only output you can manage in GAMA. Saving data to a file during an experiment can also be achieved in several ways, depending on the needs of the modeler. One way is provided by the 'save' statement, which can be used everywhere in a model or a species. The other way, described here, is to include an output_file statement in the output section.

```
output_file name:"file_name" type:file_type data:data_to_write; 
```

with:

`file_type`: text, csv or xml
`file_name`: string
`data_to_write`: string

## Example:

```
file name: "results" type: text data: time + "; " + nb_preys + ";" + nb_predators refresh_every: 2;  
```

Each time step (or according to the frequency defined in the `refresh_every` facet of the file output), a new line will be added at the end of the file. If `rewrite: false` is defined in its facets, a new file will be created for each simulation (identified by a timestamp in its name).

Optionally, a `footer` and a `header` can also be described with the corresponding facets (of type string).

NB: image files can be exported also through the `autosave` facet of the display, as explained in [this previous part](DefiningDisplaysGeneralities#displays-and-layers).
[//]: # (endConcept|export_files)