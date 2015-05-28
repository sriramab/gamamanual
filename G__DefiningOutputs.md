# Defining Outputs (Under Construction)
<font color='red'><i>todo</i>:<br>
<ul><li>explain that output can also contain file statements, monitors and inspectors (not only display)<br>
</li><li>explain the difference between 'output' and 'permanent'<br>
</li><li>explain that the 'context', in output, is that of the simulation (i.e. no need to call "simulation.var" each time)<br>
</font>
<hr /></li></ul>




Output blocks define how to visualize a simulation (with one or more display blocks that define separate windows)
```
experiment exp_name type: gui {
   [input]
   output {
     [display statements]
     [monitor statements]
     [file statements]
   }
}
```