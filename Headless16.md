# Introduction

The aim of this feature is to run models and experiments on a grid or a cluster without GUI and to take advantages of High Performance Computing. It promises efficient running by accelerating each simulation and experiment plan computing. The GUI is not loaded and managed. Several simulations could be run in parallel, at same time.

# Command

There is two ways to run a GAMA experiment in headless mode: using command-line launcher or Java command line. These commands take 2 arguments: an experiment file and an output directory.

> ## Command-line launcher
```
 sh gamaHeadless.sh $1 $2
```
  * with:
    * $1 input parameter file : an xml file determining experiment parameters and attended outputs
    * $2 output directory path : a directory which contains simulation results (numerical data and simulation snapshot)



> ## java command
```
java -Xms40m -Xmx512m -jar ./plugins/org.eclipse.equinox.launcher_1.2.0.v20110502.jar  -consoleLog  -nosplash  -application msi.gama.headless.id4 $1 $2
```
  * with:
    * $1 input parameter file: an xml file determining experiment parameters and attended outputs
    * $2 output directory path: a directory which contains simulation results (numerical data and simulation snapshot)

Note that, output directory is created during simulation and must not exist before.

# Input Experiment File

The XML input file contains for example:
```
<?xml version="1.0" encoding="UTF-8"?>
<Simulation id="2" driver="msi.gama.headless.runtime.GamaSimulator" sourcePath="./predatorPrey/predatorPrey.gaml" finalstep="1000" experiment="predPrey">
  <Parameters>
    <Parameter name="nb_predator_init" type="INT" value="53" />
    <Parameter name="nb_preys_init" type="INT" value="621" />
  </Parameters>
  <Outputs>
    <Output id="1" name="main_display" framerate="10" />
    <Output id="2" name="number_of_preys" framerate="1" />
    <Output id="3" name="number_of_predators" framerate="1" />
    <Output id="4" name="duration" framerate="1" />
  </Outputs>
</Simulation>
```

> ## Heading part

```
<Simulation id="2" driver="msi.gama.headless.runtime.GamaSimulator" sourcePath="./predatorPrey/predatorPrey.gaml" finalstep="1000" experiment="predPrey">
```

  * with:
    * **id**: permits to prefix output files for experiment plan with huge simulations.
    * **driver**: manages gama version (must not be changed)
    * **sourcePath**: contains the relative or absolute path to read the gaml model.
    * **finalstep**: determines the number of simulation step you want to run.
    * **experiment**: determines which experiment should be run on the model. This experiment should exist, otherwise the headless mode will exit.

> ## Parameters part
One line per parameter you want to specify a value:
```
<Parameter name="nb_predator_init" type="INT" value="53" />
```
  * with:
    * **name**:  name of the parameter in the gaml model
    * **type**:  type of the parameter (INT, FLOAT, BOOLEAN, STRING)
    * **value**: the chosen value

> ## Outputs part
One line per output value you want to retrieve. Outputs can be names of monitors or displays defined in the 'output' section of experiments, or the names of attributes defined in the experiment or the model itself (in the 'global' section).
```
    … with the name of a monitor defined in the 'output' section of the experiment...
    <Output id="2" name="number_of_preys" framerate="1" />
    ….with the name of a (built-in) variable defined in the experiment itself…
    <Output id="4" name="duration" framerate="1" />
```
  * with:
    * **name** : name of the output in the 'output'/'permanent' section in the experiment or name of the experiment/model attribute to retrieve
    * **framerate** : the frequency of the monitoring (each step, each 2 steps,  each 100 steps...).

  * Note that :
    * the lower the framerate value the longer the experiment.
    * if the chosen output is a display, an image is produced and the output file contains the path to access this image

# Outputs directory
During headless experiments, a directory is created with the following structure :
```
Outputed-directory-path/
    |-simulation-output.xml
    |- snapshot
          |- main_display2-0.png
          |- main_display2-10.png
          |- ...

```

  * with:
    * **simulation-output.xml**: containing the results
    * **snapshot**: containing the snapshots produced during the simulation

> ## simulation-output.xml file

```
<?xml version="1.0" encoding="UTF-8"?>
<Simulation id="2" >
	<Step id='0' >
		<Variable name='main_display' value='main_display2-0.png'/>
		<Variable name='number_of_preys' value='613'/>
		<Variable name='number_of_predators' value='51'/>
                <Variable name='duration' value='6' />
	</Step>
	<Step id='1' >
		<Variable name='main_display' value='main_display2-0.png'/>
		<Variable name='number_of_preys' value='624'/>
		<Variable name='number_of_predators' value='51'/>
                <Variable name='duration' value='5' />
	</Step>
        <Step id='2'>

...
```
  * with:
    * `<Simulation id="2" >` : block containing results of the simulation 2 (this Id is identified in the Input Experiment File)
    * `<Step id='1' > ... </Step>`: one block per step done. the id corresponds to the step number

> ### Step block
```
	<Step id='1' >
		<Variable name='main_display' value='main_display2-0.png'/>
		<Variable name='number_of_preys' value='624'/>
		<Variable name='number_of_predators' value='51'/>
                <Variable name='duration' value='6' />
	</Step>

```

There is one Variable block per Output identified in the output experiment file.

> ### Variable block

```
 <Variable name='main_display' value='main_display2-0.png'/>
```
  * with:
    * **name**: name of the output, the model variable
    * **value**: the current value of model variable.

Note that the value of an output is repeated according to the framerate defined in the input experiment file.

> ## Snapshot files
This directory contains images generated during the experiment. There is one image per displayed output per step (according to the framerate). File names follow a naming convention, e.g:
```
   [outputName][SimulationID]_[stepID].png -> main_display2-20.png
```

Note that images will be saved in the '.png' format.