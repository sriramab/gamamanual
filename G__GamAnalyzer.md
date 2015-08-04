GamAnalyzer is a tool to monitor several multi-agents simulation

# Install
You need to run the SVN version.

# An introduction to GamAnalyzer

The "agent_group_follower" goal is to monitor and analyze a group of agent during several simulation. This group of agent can be chosen by the user according to criteria chosen by the user. The monitoring process and analysis of these agents involves the extraction, processing and visualization of their data at every step of the simulation.  The data for each simulation are pooled and treated commonly for their graphic representation or clusters.

# Storable Data
**StorableData** store in matrices data extracted directly from agents, but also calculate statistics (minimum, maximum, average, ...). Matrices and maps that has a StorableData are:

## meta_data_history

Matrix "metadata" of the simulation: with every step (line), gives the identifier, the number of agents, listing agents, etc. (column)

```
updateMetaDataHistory(scope);
```

## last_detailed_var_values

matrice des valeurs de toutes les variables (numériques ou non) (en colonne) pour chaque agent (ligne)

## average_history
matrice des moyennes : donne pour chaque variable numérique (colonne), à chaque pas (ligne), la moyenne correspondante

## stdev_history
matrices des écart-type 

## min_history
matrice des minimums public GamaFloatMatrix max_history; // matrice des maximums

## distrib_history
matrice de la distribution des variables des agents (colonne) à chaque pas (ligne), sur les intervalles donnés par « distrib_history_params »

## GamaObjectMatrix distrib_history_params
les valeurs des intervalles considérés par « distribhistory », pour chaque variable (colonne) à chaque pas (ligne)


# Example on road traffic

This example will be based on the Road Traffic model which is composed of roads, buildings and people. In this example we will use GamAnalyzer to follow the agent people. 

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
