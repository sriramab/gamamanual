GamAnalyzer is a tool to monitor several multi-agents simulation

# Install
You need to run the SVN version.

# An introduction to GamAnalyzer

The "agent_group_follower" goal is to monitor and analyze a group of agent during several simulation. This group of agent can be chosen by the user according to criteria chosen by the user. The monitoring process and analysis of these agents involves the extraction, processing and visualization of their data at every step of the simulation.  The data for each simulation are pooled and treated commonly for their graphic representation or clusters.

# Example 

This example is based on a toy model which is only composed of wandering people. In this example we will use GamAnalyzer to follow the agent people. 

## 
```
agent_group_follower peoplefollower;
```
```
create agentfollower 
{
  do analyse_cluster species_to_analyse:"people";
  peoplefollower<-self;
}
```

## expGlobalNone: No clustering only the current agent follower is displayed
```
aspect base {
  display_mode <-"global";
  clustering_mode <-"none";
  draw shape color: #red;
}
```

## expSimGlobalNone 
