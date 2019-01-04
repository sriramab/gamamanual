# Operators (B to C)
 	


## Definition 

Operators in the GAML language are used to compose complex expressions. An operator performs a function on one, two, or n operands (which are other expressions and thus may be themselves composed of operators) and returns the result of this function. 

Most of them use a classical prefixed functional syntax (i.e. `operator_name(operand1, operand2, operand3)`, see below), with the exception of arithmetic (e.g. `+`, `/`), logical (`and`, `or`), comparison (e.g. `>`, `<`), access (`.`, `[..]`) and pair (`::`) operators, which require an infixed notation (i.e. `operand1 operator_symbol operand1`). 

The ternary functional if-else operator, `? :`, uses a special infixed syntax composed with two symbols (e.g. `operand1 ? operand2 : operand3`). Two unary operators (`-` and `!`) use a traditional prefixed syntax that does not require parentheses unless the operand is itself a complex expression (e.g. ` - 10`, `! (operand1 or operand2)`). 

Finally, special constructor operators (`{...}` for constructing points, `[...]` for constructing lists and maps) will require their operands to be placed between their two symbols (e.g. `{1,2,3}`, `[operand1, operand2, ..., operandn]` or `[key1::value1, key2::value2... keyn::valuen]`).

With the exception of these special cases above, the following rules apply to the syntax of operators:
* if they only have one operand, the functional prefixed syntax is mandatory (e.g. `operator_name(operand1)`)
* if they have two arguments, either the functional prefixed syntax (e.g. `operator_name(operand1, operand2)`) or the infixed syntax (e.g. `operand1 operator_name operand2`) can be used.
* if they have more than two arguments, either the functional prefixed syntax (e.g. `operator_name(operand1, operand2, ..., operand)`) or a special infixed syntax with the first operand on the left-hand side of the operator name (e.g. `operand1 operator_name(operand2, ..., operand)`) can be used.

All of these alternative syntaxes are completely equivalent.

Operators in GAML are purely functional, i.e. they are guaranteed to not have any side effects on their operands. For instance, the `shuffle` operator, which randomizes the positions of elements in a list, does not modify its list operand but returns a new shuffled list.


----

## Priority between operators

The priority of operators determines, in the case of complex expressions composed of several operators, which one(s) will be evaluated first.

GAML follows in general the traditional priorities attributed to arithmetic, boolean, comparison operators, with some twists. Namely:
* the constructor operators, like `::`, used to compose pairs of operands, have the lowest priority of all operators (e.g. `a > b :: b > c` will return a pair of boolean values, which means that the two comparisons are evaluated before the operator applies. Similarly, `[a > 10, b > 5]` will return a list of boolean values.
* it is followed by the `?:` operator, the functional if-else (e.g. ` a > b ? a + 10 : a - 10` will return the result of the if-else).
* next are the logical operators, `and` and `or` (e.g. `a > b or b > c` will return the value of the test)
* next are the comparison operators (i.e. `>`, `<`, `<=`, `>=`, `=`, `!=`)
* next the arithmetic operators in their logical order (multiplicative operators have a higher priority than additive operators)
* next the unary operators `-` and `!`
* next the access operators `.` and `[]` (e.g. `{1,2,3}.x > 20 + {4,5,6}.y` will return the result of the comparison between the x and y ordinates of the two points)
* and finally the functional operators, which have the highest priority of all.

----

## Using actions as operators

Actions defined in species can be used as operators, provided they are called on the correct agent. The syntax is that of normal functional operators, but the agent that will perform the action must be added as the first operand.

For instance, if the following species is defined:

```
species spec1 {
        int min(int x, int y) {
                return x > y ? x : y;
        }
}
```

Any agent instance of spec1 can use `min` as an operator (if the action conflicts with an existing operator, a warning will be emitted). For instance, in the same model, the following line is perfectly acceptable:

```
global {
        init {
                create spec1;
                spec1 my_agent <- spec1[0];
                int the_min <- my_agent min(10,20); // or min(my_agent, 10, 20);
        }
}
```

If the action doesn't have any operands, the syntax to use is `my_agent the_action()`. Finally, if it does not return a value, it might still be used but is considering as returning a value of type `unknown` (e.g. `unknown result <- my_agent the_action(op1, op2);`).

Note that due to the fact that actions are written by modelers, the general functional contract is not respected in that case: actions might perfectly have side effects on their operands (including the agent).

	

----

## Table of Contents

----

## Operators by categories
	

----

### 3D
[box](OperatorsBC#box), [cone3D](OperatorsBC#cone3d), [cube](OperatorsBC#cube), [cylinder](OperatorsBC#cylinder), [dem](OperatorsDH#dem), [hexagon](OperatorsDH#hexagon), [pyramid](OperatorsNR#pyramid), [rgb_to_xyz](OperatorsNR#rgb_to_xyz), [set_z](OperatorsSZ#set_z), [sphere](OperatorsSZ#sphere), [teapot](OperatorsSZ#teapot), 

----

### Arithmetic operators
[-](OperatorsAA#-), [/](OperatorsAA#/), [^](OperatorsAA#^), [*](OperatorsAA#*), [+](OperatorsAA#+), [abs](OperatorsAA#abs), [acos](OperatorsAA#acos), [asin](OperatorsAA#asin), [atan](OperatorsAA#atan), [atan2](OperatorsAA#atan2), [ceil](OperatorsBC#ceil), [cos](OperatorsBC#cos), [cos_rad](OperatorsBC#cos_rad), [div](OperatorsDH#div), [even](OperatorsDH#even), [exp](OperatorsDH#exp), [fact](OperatorsDH#fact), [floor](OperatorsDH#floor), [hypot](OperatorsDH#hypot), [is_finite](OperatorsIM#is_finite), [is_number](OperatorsIM#is_number), [ln](OperatorsIM#ln), [log](OperatorsIM#log), [mod](OperatorsIM#mod), [round](OperatorsNR#round), [signum](OperatorsSZ#signum), [sin](OperatorsSZ#sin), [sin_rad](OperatorsSZ#sin_rad), [sqrt](OperatorsSZ#sqrt), [tan](OperatorsSZ#tan), [tan_rad](OperatorsSZ#tan_rad), [tanh](OperatorsSZ#tanh), [with_precision](OperatorsSZ#with_precision), 

----

### BDI
[and](OperatorsAA#and), [eval_when](OperatorsDH#eval_when), [get_about](OperatorsDH#get_about), [get_agent](OperatorsDH#get_agent), [get_agent_cause](OperatorsDH#get_agent_cause), [get_belief_op](OperatorsDH#get_belief_op), [get_belief_with_name_op](OperatorsDH#get_belief_with_name_op), [get_beliefs_op](OperatorsDH#get_beliefs_op), [get_beliefs_with_name_op](OperatorsDH#get_beliefs_with_name_op), [get_current_intention_op](OperatorsDH#get_current_intention_op), [get_decay](OperatorsDH#get_decay), [get_desire_op](OperatorsDH#get_desire_op), [get_desire_with_name_op](OperatorsDH#get_desire_with_name_op), [get_desires_op](OperatorsDH#get_desires_op), [get_desires_with_name_op](OperatorsDH#get_desires_with_name_op), [get_dominance](OperatorsDH#get_dominance), [get_familiarity](OperatorsDH#get_familiarity), [get_ideal_op](OperatorsDH#get_ideal_op), [get_ideal_with_name_op](OperatorsDH#get_ideal_with_name_op), [get_ideals_op](OperatorsDH#get_ideals_op), [get_ideals_with_name_op](OperatorsDH#get_ideals_with_name_op), [get_intensity](OperatorsDH#get_intensity), [get_intention_op](OperatorsDH#get_intention_op), [get_intention_with_name_op](OperatorsDH#get_intention_with_name_op), [get_intentions_op](OperatorsDH#get_intentions_op), [get_intentions_with_name_op](OperatorsDH#get_intentions_with_name_op), [get_lifetime](OperatorsDH#get_lifetime), [get_liking](OperatorsDH#get_liking), [get_modality](OperatorsDH#get_modality), [get_obligation_op](OperatorsDH#get_obligation_op), [get_obligation_with_name_op](OperatorsDH#get_obligation_with_name_op), [get_obligations_op](OperatorsDH#get_obligations_op), [get_obligations_with_name_op](OperatorsDH#get_obligations_with_name_op), [get_plan_name](OperatorsDH#get_plan_name), [get_predicate](OperatorsDH#get_predicate), [get_solidarity](OperatorsDH#get_solidarity), [get_strength](OperatorsDH#get_strength), [get_super_intention](OperatorsDH#get_super_intention), [get_trust](OperatorsDH#get_trust), [get_truth](OperatorsDH#get_truth), [get_uncertainties_op](OperatorsDH#get_uncertainties_op), [get_uncertainties_with_name_op](OperatorsDH#get_uncertainties_with_name_op), [get_uncertainty_op](OperatorsDH#get_uncertainty_op), [get_uncertainty_with_name_op](OperatorsDH#get_uncertainty_with_name_op), [has_belief_op](OperatorsDH#has_belief_op), [has_belief_with_name_op](OperatorsDH#has_belief_with_name_op), [has_desire_op](OperatorsDH#has_desire_op), [has_desire_with_name_op](OperatorsDH#has_desire_with_name_op), [has_ideal_op](OperatorsDH#has_ideal_op), [has_ideal_with_name_op](OperatorsDH#has_ideal_with_name_op), [has_intention_op](OperatorsDH#has_intention_op), [has_intention_with_name_op](OperatorsDH#has_intention_with_name_op), [has_obligation_op](OperatorsDH#has_obligation_op), [has_obligation_with_name_op](OperatorsDH#has_obligation_with_name_op), [has_uncertainty_op](OperatorsDH#has_uncertainty_op), [has_uncertainty_with_name_op](OperatorsDH#has_uncertainty_with_name_op), [new_emotion](OperatorsNR#new_emotion), [new_mental_state](OperatorsNR#new_mental_state), [new_predicate](OperatorsNR#new_predicate), [new_social_link](OperatorsNR#new_social_link), [or](OperatorsNR#or), [set_about](OperatorsSZ#set_about), [set_agent](OperatorsSZ#set_agent), [set_agent_cause](OperatorsSZ#set_agent_cause), [set_decay](OperatorsSZ#set_decay), [set_dominance](OperatorsSZ#set_dominance), [set_familiarity](OperatorsSZ#set_familiarity), [set_intensity](OperatorsSZ#set_intensity), [set_lifetime](OperatorsSZ#set_lifetime), [set_liking](OperatorsSZ#set_liking), [set_modality](OperatorsSZ#set_modality), [set_predicate](OperatorsSZ#set_predicate), [set_solidarity](OperatorsSZ#set_solidarity), [set_strength](OperatorsSZ#set_strength), [set_trust](OperatorsSZ#set_trust), [set_truth](OperatorsSZ#set_truth), [with_lifetime](OperatorsSZ#with_lifetime), [with_values](OperatorsSZ#with_values), 

----

### Casting operators
[as](OperatorsAA#as), [as_int](OperatorsAA#as_int), [as_matrix](OperatorsAA#as_matrix), [font](OperatorsDH#font), [is](OperatorsIM#is), [is_skill](OperatorsIM#is_skill), [list_with](OperatorsIM#list_with), [matrix_with](OperatorsIM#matrix_with), [species](OperatorsSZ#species), [to_gaml](OperatorsSZ#to_gaml), [topology](OperatorsSZ#topology), 

----

### Color-related operators
[-](OperatorsAA#-), [/](OperatorsAA#/), [*](OperatorsAA#*), [+](OperatorsAA#+), [blend](OperatorsBC#blend), [brewer_colors](OperatorsBC#brewer_colors), [brewer_palettes](OperatorsBC#brewer_palettes), [grayscale](OperatorsDH#grayscale), [hsb](OperatorsDH#hsb), [mean](OperatorsIM#mean), [median](OperatorsIM#median), [rgb](OperatorsNR#rgb), [rnd_color](OperatorsNR#rnd_color), [sum](OperatorsSZ#sum), 

----

### Comparison operators
[!=](OperatorsAA#!=), [<](OperatorsAA#<), [<=](OperatorsAA#<=), [=](OperatorsAA#=), [>](OperatorsAA#>), [>=](OperatorsAA#>=), [between](OperatorsBC#between), 

----

### Containers-related operators
[-](OperatorsAA#-), [::](OperatorsAA#::), [+](OperatorsAA#+), [accumulate](OperatorsAA#accumulate), [among](OperatorsAA#among), [at](OperatorsAA#at), [collect](OperatorsBC#collect), [contains](OperatorsBC#contains), [contains_all](OperatorsBC#contains_all), [contains_any](OperatorsBC#contains_any), [count](OperatorsBC#count), [distinct](OperatorsDH#distinct), [empty](OperatorsDH#empty), [every](OperatorsDH#every), [first](OperatorsDH#first), [first_with](OperatorsDH#first_with), [get](OperatorsDH#get), [group_by](OperatorsDH#group_by), [in](OperatorsIM#in), [index_by](OperatorsIM#index_by), [inter](OperatorsIM#inter), [interleave](OperatorsIM#interleave), [internal_at](OperatorsIM#internal_at), [internal_integrated_value](OperatorsIM#internal_integrated_value), [last](OperatorsIM#last), [last_with](OperatorsIM#last_with), [length](OperatorsIM#length), [max](OperatorsIM#max), [max_of](OperatorsIM#max_of), [mean](OperatorsIM#mean), [mean_of](OperatorsIM#mean_of), [median](OperatorsIM#median), [min](OperatorsIM#min), [min_of](OperatorsIM#min_of), [mul](OperatorsIM#mul), [one_of](OperatorsNR#one_of), [product_of](OperatorsNR#product_of), [range](OperatorsNR#range), [reverse](OperatorsNR#reverse), [shuffle](OperatorsSZ#shuffle), [sort_by](OperatorsSZ#sort_by), [split](OperatorsSZ#split), [split_in](OperatorsSZ#split_in), [split_using](OperatorsSZ#split_using), [sum](OperatorsSZ#sum), [sum_of](OperatorsSZ#sum_of), [union](OperatorsSZ#union), [variance_of](OperatorsSZ#variance_of), [where](OperatorsSZ#where), [with_max_of](OperatorsSZ#with_max_of), [with_min_of](OperatorsSZ#with_min_of), 

----

### Date-related operators
[-](OperatorsAA#-), [!=](OperatorsAA#!=), [+](OperatorsAA#+), [<](OperatorsAA#<), [<=](OperatorsAA#<=), [=](OperatorsAA#=), [>](OperatorsAA#>), [>=](OperatorsAA#>=), [after](OperatorsAA#after), [before](OperatorsBC#before), [between](OperatorsBC#between), [every](OperatorsDH#every), [milliseconds_between](OperatorsIM#milliseconds_between), [minus_days](OperatorsIM#minus_days), [minus_hours](OperatorsIM#minus_hours), [minus_minutes](OperatorsIM#minus_minutes), [minus_months](OperatorsIM#minus_months), [minus_ms](OperatorsIM#minus_ms), [minus_weeks](OperatorsIM#minus_weeks), [minus_years](OperatorsIM#minus_years), [months_between](OperatorsIM#months_between), [plus_days](OperatorsNR#plus_days), [plus_hours](OperatorsNR#plus_hours), [plus_minutes](OperatorsNR#plus_minutes), [plus_months](OperatorsNR#plus_months), [plus_ms](OperatorsNR#plus_ms), [plus_weeks](OperatorsNR#plus_weeks), [plus_years](OperatorsNR#plus_years), [since](OperatorsSZ#since), [to](OperatorsSZ#to), [until](OperatorsSZ#until), [years_between](OperatorsSZ#years_between), 

----

### Dates


----

### DescriptiveStatistics
[auto_correlation](OperatorsAA#auto_correlation), [correlation](OperatorsBC#correlation), [covariance](OperatorsBC#covariance), [durbin_watson](OperatorsDH#durbin_watson), [kurtosis](OperatorsIM#kurtosis), [moment](OperatorsIM#moment), [quantile](OperatorsNR#quantile), [quantile_inverse](OperatorsNR#quantile_inverse), [rank_interpolated](OperatorsNR#rank_interpolated), [rms](OperatorsNR#rms), [skew](OperatorsSZ#skew), [variance](OperatorsSZ#variance), 

----

### Displays
[horizontal](OperatorsDH#horizontal), [stack](OperatorsSZ#stack), [vertical](OperatorsSZ#vertical), 

----

### Distributions
[binomial_coeff](OperatorsBC#binomial_coeff), [binomial_complemented](OperatorsBC#binomial_complemented), [binomial_sum](OperatorsBC#binomial_sum), [chi_square](OperatorsBC#chi_square), [chi_square_complemented](OperatorsBC#chi_square_complemented), [gamma_distribution](OperatorsDH#gamma_distribution), [gamma_distribution_complemented](OperatorsDH#gamma_distribution_complemented), [normal_area](OperatorsNR#normal_area), [normal_density](OperatorsNR#normal_density), [normal_inverse](OperatorsNR#normal_inverse), [pValue_for_fStat](OperatorsNR#pvalue_for_fstat), [pValue_for_tStat](OperatorsNR#pvalue_for_tstat), [student_area](OperatorsSZ#student_area), [student_t_inverse](OperatorsSZ#student_t_inverse), 

----

### Driving operators
[as_driving_graph](OperatorsAA#as_driving_graph), 

----

### edge
[edge_between](OperatorsDH#edge_between), [strahler](OperatorsSZ#strahler), 

----

### EDP-related operators
[diff](OperatorsDH#diff), [diff2](OperatorsDH#diff2), [internal_zero_order_equation](OperatorsIM#internal_zero_order_equation), 

----

### Files-related operators
[crs](OperatorsBC#crs), [evaluate_sub_model](OperatorsDH#evaluate_sub_model), [file](OperatorsDH#file), [file_exists](OperatorsDH#file_exists), [folder](OperatorsDH#folder), [get](OperatorsDH#get), [load_sub_model](OperatorsIM#load_sub_model), [new_folder](OperatorsNR#new_folder), [osm_file](OperatorsNR#osm_file), [read](OperatorsNR#read), [step_sub_model](OperatorsSZ#step_sub_model), [writable](OperatorsSZ#writable), 

----

### FIPA-related operators
[conversation](OperatorsBC#conversation), [message](OperatorsIM#message), 

----

### GamaMetaType
[type_of](OperatorsSZ#type_of), 

----

### GammaFunction
[beta](OperatorsBC#beta), [gamma](OperatorsDH#gamma), [incomplete_beta](OperatorsIM#incomplete_beta), [incomplete_gamma](OperatorsIM#incomplete_gamma), [incomplete_gamma_complement](OperatorsIM#incomplete_gamma_complement), [log_gamma](OperatorsIM#log_gamma), 

----

### Graphs-related operators
[add_edge](OperatorsAA#add_edge), [add_node](OperatorsAA#add_node), [adjacency](OperatorsAA#adjacency), [agent_from_geometry](OperatorsAA#agent_from_geometry), [all_pairs_shortest_path](OperatorsAA#all_pairs_shortest_path), [alpha_index](OperatorsAA#alpha_index), [as_distance_graph](OperatorsAA#as_distance_graph), [as_edge_graph](OperatorsAA#as_edge_graph), [as_intersection_graph](OperatorsAA#as_intersection_graph), [as_path](OperatorsAA#as_path), [beta_index](OperatorsBC#beta_index), [betweenness_centrality](OperatorsBC#betweenness_centrality), [biggest_cliques_of](OperatorsBC#biggest_cliques_of), [connected_components_of](OperatorsBC#connected_components_of), [connectivity_index](OperatorsBC#connectivity_index), [contains_edge](OperatorsBC#contains_edge), [contains_vertex](OperatorsBC#contains_vertex), [degree_of](OperatorsDH#degree_of), [directed](OperatorsDH#directed), [edge](OperatorsDH#edge), [edge_between](OperatorsDH#edge_between), [edge_betweenness](OperatorsDH#edge_betweenness), [edges](OperatorsDH#edges), [gamma_index](OperatorsDH#gamma_index), [generate_barabasi_albert](OperatorsDH#generate_barabasi_albert), [generate_complete_graph](OperatorsDH#generate_complete_graph), [generate_watts_strogatz](OperatorsDH#generate_watts_strogatz), [grid_cells_to_graph](OperatorsDH#grid_cells_to_graph), [in_degree_of](OperatorsIM#in_degree_of), [in_edges_of](OperatorsIM#in_edges_of), [layout](OperatorsIM#layout), [load_graph_from_file](OperatorsIM#load_graph_from_file), [load_shortest_paths](OperatorsIM#load_shortest_paths), [main_connected_component](OperatorsIM#main_connected_component), [max_flow_between](OperatorsIM#max_flow_between), [maximal_cliques_of](OperatorsIM#maximal_cliques_of), [nb_cycles](OperatorsNR#nb_cycles), [neighbors_of](OperatorsNR#neighbors_of), [node](OperatorsNR#node), [nodes](OperatorsNR#nodes), [out_degree_of](OperatorsNR#out_degree_of), [out_edges_of](OperatorsNR#out_edges_of), [path_between](OperatorsNR#path_between), [paths_between](OperatorsNR#paths_between), [predecessors_of](OperatorsNR#predecessors_of), [remove_node_from](OperatorsNR#remove_node_from), [rewire_n](OperatorsNR#rewire_n), [source_of](OperatorsSZ#source_of), [spatial_graph](OperatorsSZ#spatial_graph), [strahler](OperatorsSZ#strahler), [successors_of](OperatorsSZ#successors_of), [sum](OperatorsSZ#sum), [target_of](OperatorsSZ#target_of), [undirected](OperatorsSZ#undirected), [use_cache](OperatorsSZ#use_cache), [weight_of](OperatorsSZ#weight_of), [with_optimizer_type](OperatorsSZ#with_optimizer_type), [with_weights](OperatorsSZ#with_weights), 

----

### Grid-related operators
[as_4_grid](OperatorsAA#as_4_grid), [as_grid](OperatorsAA#as_grid), [as_hexagonal_grid](OperatorsAA#as_hexagonal_grid), [grid_at](OperatorsDH#grid_at), [path_between](OperatorsNR#path_between), 

----

### Iterator operators
[accumulate](OperatorsAA#accumulate), [as_map](OperatorsAA#as_map), [collect](OperatorsBC#collect), [count](OperatorsBC#count), [create_map](OperatorsBC#create_map), [distribution_of](OperatorsDH#distribution_of), [distribution_of](OperatorsDH#distribution_of), [distribution_of](OperatorsDH#distribution_of), [distribution2d_of](OperatorsDH#distribution2d_of), [distribution2d_of](OperatorsDH#distribution2d_of), [distribution2d_of](OperatorsDH#distribution2d_of), [first_with](OperatorsDH#first_with), [frequency_of](OperatorsDH#frequency_of), [group_by](OperatorsDH#group_by), [index_by](OperatorsIM#index_by), [last_with](OperatorsIM#last_with), [max_of](OperatorsIM#max_of), [mean_of](OperatorsIM#mean_of), [min_of](OperatorsIM#min_of), [product_of](OperatorsNR#product_of), [sort_by](OperatorsSZ#sort_by), [sum_of](OperatorsSZ#sum_of), [variance_of](OperatorsSZ#variance_of), [where](OperatorsSZ#where), [with_max_of](OperatorsSZ#with_max_of), [with_min_of](OperatorsSZ#with_min_of), 

----

### List-related operators
[copy_between](OperatorsBC#copy_between), [index_of](OperatorsIM#index_of), [last_index_of](OperatorsIM#last_index_of), 

----

### Logical operators
[:](OperatorsAA#:), [!](OperatorsAA#!), [?](OperatorsAA#?), [add_3Dmodel](OperatorsAA#add_3dmodel), [add_geometry](OperatorsAA#add_geometry), [add_icon](OperatorsAA#add_icon), [and](OperatorsAA#and), [or](OperatorsNR#or), [xor](OperatorsSZ#xor), 

----

### Map comparaison operators
[fuzzy_kappa](OperatorsDH#fuzzy_kappa), [fuzzy_kappa_sim](OperatorsDH#fuzzy_kappa_sim), [kappa](OperatorsIM#kappa), [kappa_sim](OperatorsIM#kappa_sim), [percent_absolute_deviation](OperatorsNR#percent_absolute_deviation), 

----

### Map-related operators
[as_map](OperatorsAA#as_map), [create_map](OperatorsBC#create_map), [index_of](OperatorsIM#index_of), [last_index_of](OperatorsIM#last_index_of), 

----

### Material
[material](OperatorsIM#material), 

----

### Matrix-related operators
[-](OperatorsAA#-), [/](OperatorsAA#/), [.](OperatorsAA#.), [*](OperatorsAA#*), [+](OperatorsAA#+), [append_horizontally](OperatorsAA#append_horizontally), [append_vertically](OperatorsAA#append_vertically), [column_at](OperatorsBC#column_at), [columns_list](OperatorsBC#columns_list), [determinant](OperatorsDH#determinant), [eigenvalues](OperatorsDH#eigenvalues), [index_of](OperatorsIM#index_of), [inverse](OperatorsIM#inverse), [last_index_of](OperatorsIM#last_index_of), [row_at](OperatorsNR#row_at), [rows_list](OperatorsNR#rows_list), [shuffle](OperatorsSZ#shuffle), [trace](OperatorsSZ#trace), [transpose](OperatorsSZ#transpose), 

----

### multicriteria operators
[electre_DM](OperatorsDH#electre_dm), [evidence_theory_DM](OperatorsDH#evidence_theory_dm), [fuzzy_choquet_DM](OperatorsDH#fuzzy_choquet_dm), [promethee_DM](OperatorsNR#promethee_dm), [weighted_means_DM](OperatorsSZ#weighted_means_dm), 

----

### Path-related operators
[agent_from_geometry](OperatorsAA#agent_from_geometry), [all_pairs_shortest_path](OperatorsAA#all_pairs_shortest_path), [as_path](OperatorsAA#as_path), [load_shortest_paths](OperatorsIM#load_shortest_paths), [max_flow_between](OperatorsIM#max_flow_between), [path_between](OperatorsNR#path_between), [path_to](OperatorsNR#path_to), [paths_between](OperatorsNR#paths_between), [use_cache](OperatorsSZ#use_cache), 

----

### Points-related operators
[-](OperatorsAA#-), [/](OperatorsAA#/), [*](OperatorsAA#*), [+](OperatorsAA#+), [<](OperatorsAA#<), [<=](OperatorsAA#<=), [>](OperatorsAA#>), [>=](OperatorsAA#>=), [add_point](OperatorsAA#add_point), [angle_between](OperatorsAA#angle_between), [any_location_in](OperatorsAA#any_location_in), [centroid](OperatorsBC#centroid), [closest_points_with](OperatorsBC#closest_points_with), [farthest_point_to](OperatorsDH#farthest_point_to), [grid_at](OperatorsDH#grid_at), [norm](OperatorsNR#norm), [points_along](OperatorsNR#points_along), [points_at](OperatorsNR#points_at), [points_on](OperatorsNR#points_on), 

----

### Random operators
[binomial](OperatorsBC#binomial), [flip](OperatorsDH#flip), [gauss](OperatorsDH#gauss), [improved_generator](OperatorsIM#improved_generator), [open_simplex_generator](OperatorsNR#open_simplex_generator), [poisson](OperatorsNR#poisson), [rnd](OperatorsNR#rnd), [rnd_choice](OperatorsNR#rnd_choice), [sample](OperatorsSZ#sample), [shuffle](OperatorsSZ#shuffle), [simplex_generator](OperatorsSZ#simplex_generator), [skew_gauss](OperatorsSZ#skew_gauss), [truncated_gauss](OperatorsSZ#truncated_gauss), 

----

### ReverseOperators
[restoreSimulation](OperatorsNR#restoresimulation), [restoreSimulationFromFile](OperatorsNR#restoresimulationfromfile), [saveAgent](OperatorsSZ#saveagent), [saveSimulation](OperatorsSZ#savesimulation), [serialize](OperatorsSZ#serialize), [serializeAgent](OperatorsSZ#serializeagent), 

----

### Shape
[arc](OperatorsAA#arc), [box](OperatorsBC#box), [circle](OperatorsBC#circle), [cone](OperatorsBC#cone), [cone3D](OperatorsBC#cone3d), [cross](OperatorsBC#cross), [cube](OperatorsBC#cube), [curve](OperatorsBC#curve), [cylinder](OperatorsBC#cylinder), [ellipse](OperatorsDH#ellipse), [envelope](OperatorsDH#envelope), [geometry_collection](OperatorsDH#geometry_collection), [hexagon](OperatorsDH#hexagon), [line](OperatorsIM#line), [link](OperatorsIM#link), [plan](OperatorsNR#plan), [polygon](OperatorsNR#polygon), [polyhedron](OperatorsNR#polyhedron), [pyramid](OperatorsNR#pyramid), [rectangle](OperatorsNR#rectangle), [sphere](OperatorsSZ#sphere), [square](OperatorsSZ#square), [squircle](OperatorsSZ#squircle), [teapot](OperatorsSZ#teapot), [triangle](OperatorsSZ#triangle), 

----

### Spatial operators
[-](OperatorsAA#-), [*](OperatorsAA#*), [+](OperatorsAA#+), [add_point](OperatorsAA#add_point), [agent_closest_to](OperatorsAA#agent_closest_to), [agent_farthest_to](OperatorsAA#agent_farthest_to), [agents_at_distance](OperatorsAA#agents_at_distance), [agents_inside](OperatorsAA#agents_inside), [agents_overlapping](OperatorsAA#agents_overlapping), [angle_between](OperatorsAA#angle_between), [any_location_in](OperatorsAA#any_location_in), [arc](OperatorsAA#arc), [around](OperatorsAA#around), [as_4_grid](OperatorsAA#as_4_grid), [as_grid](OperatorsAA#as_grid), [as_hexagonal_grid](OperatorsAA#as_hexagonal_grid), [at_distance](OperatorsAA#at_distance), [at_location](OperatorsAA#at_location), [box](OperatorsBC#box), [centroid](OperatorsBC#centroid), [circle](OperatorsBC#circle), [clean](OperatorsBC#clean), [clean_network](OperatorsBC#clean_network), [closest_points_with](OperatorsBC#closest_points_with), [closest_to](OperatorsBC#closest_to), [cone](OperatorsBC#cone), [cone3D](OperatorsBC#cone3d), [convex_hull](OperatorsBC#convex_hull), [covers](OperatorsBC#covers), [cross](OperatorsBC#cross), [crosses](OperatorsBC#crosses), [crs](OperatorsBC#crs), [CRS_transform](OperatorsBC#crs_transform), [cube](OperatorsBC#cube), [curve](OperatorsBC#curve), [cylinder](OperatorsBC#cylinder), [dem](OperatorsDH#dem), [direction_between](OperatorsDH#direction_between), [disjoint_from](OperatorsDH#disjoint_from), [distance_between](OperatorsDH#distance_between), [distance_to](OperatorsDH#distance_to), [ellipse](OperatorsDH#ellipse), [envelope](OperatorsDH#envelope), [farthest_point_to](OperatorsDH#farthest_point_to), [farthest_to](OperatorsDH#farthest_to), [geometry_collection](OperatorsDH#geometry_collection), [gini](OperatorsDH#gini), [hexagon](OperatorsDH#hexagon), [hierarchical_clustering](OperatorsDH#hierarchical_clustering), [IDW](OperatorsIM#idw), [inside](OperatorsIM#inside), [inter](OperatorsIM#inter), [intersects](OperatorsIM#intersects), [line](OperatorsIM#line), [link](OperatorsIM#link), [masked_by](OperatorsIM#masked_by), [moran](OperatorsIM#moran), [neighbors_at](OperatorsNR#neighbors_at), [neighbors_of](OperatorsNR#neighbors_of), [overlapping](OperatorsNR#overlapping), [overlaps](OperatorsNR#overlaps), [partially_overlaps](OperatorsNR#partially_overlaps), [path_between](OperatorsNR#path_between), [path_to](OperatorsNR#path_to), [plan](OperatorsNR#plan), [points_along](OperatorsNR#points_along), [points_at](OperatorsNR#points_at), [points_on](OperatorsNR#points_on), [polygon](OperatorsNR#polygon), [polyhedron](OperatorsNR#polyhedron), [pyramid](OperatorsNR#pyramid), [rectangle](OperatorsNR#rectangle), [rgb_to_xyz](OperatorsNR#rgb_to_xyz), [rotated_by](OperatorsNR#rotated_by), [round](OperatorsNR#round), [scaled_to](OperatorsSZ#scaled_to), [set_z](OperatorsSZ#set_z), [simple_clustering_by_distance](OperatorsSZ#simple_clustering_by_distance), [simplification](OperatorsSZ#simplification), [skeletonize](OperatorsSZ#skeletonize), [smooth](OperatorsSZ#smooth), [sphere](OperatorsSZ#sphere), [split_at](OperatorsSZ#split_at), [split_geometry](OperatorsSZ#split_geometry), [split_lines](OperatorsSZ#split_lines), [square](OperatorsSZ#square), [squircle](OperatorsSZ#squircle), [teapot](OperatorsSZ#teapot), [to_GAMA_CRS](OperatorsSZ#to_gama_crs), [to_rectangles](OperatorsSZ#to_rectangles), [to_squares](OperatorsSZ#to_squares), [to_sub_geometries](OperatorsSZ#to_sub_geometries), [touches](OperatorsSZ#touches), [towards](OperatorsSZ#towards), [transformed_by](OperatorsSZ#transformed_by), [translated_by](OperatorsSZ#translated_by), [triangle](OperatorsSZ#triangle), [triangulate](OperatorsSZ#triangulate), [union](OperatorsSZ#union), [using](OperatorsSZ#using), [voronoi](OperatorsSZ#voronoi), [with_precision](OperatorsSZ#with_precision), [without_holes](OperatorsSZ#without_holes), 

----

### Spatial properties operators
[covers](OperatorsBC#covers), [crosses](OperatorsBC#crosses), [intersects](OperatorsIM#intersects), [partially_overlaps](OperatorsNR#partially_overlaps), [touches](OperatorsSZ#touches), 

----

### Spatial queries operators
[agent_closest_to](OperatorsAA#agent_closest_to), [agent_farthest_to](OperatorsAA#agent_farthest_to), [agents_at_distance](OperatorsAA#agents_at_distance), [agents_inside](OperatorsAA#agents_inside), [agents_overlapping](OperatorsAA#agents_overlapping), [at_distance](OperatorsAA#at_distance), [closest_to](OperatorsBC#closest_to), [farthest_to](OperatorsDH#farthest_to), [inside](OperatorsIM#inside), [neighbors_at](OperatorsNR#neighbors_at), [neighbors_of](OperatorsNR#neighbors_of), [overlapping](OperatorsNR#overlapping), 

----

### Spatial relations operators
[direction_between](OperatorsDH#direction_between), [distance_between](OperatorsDH#distance_between), [distance_to](OperatorsDH#distance_to), [path_between](OperatorsNR#path_between), [path_to](OperatorsNR#path_to), [towards](OperatorsSZ#towards), 

----

### Spatial statistical operators
[hierarchical_clustering](OperatorsDH#hierarchical_clustering), [simple_clustering_by_distance](OperatorsSZ#simple_clustering_by_distance), 

----

### Spatial transformations operators
[-](OperatorsAA#-), [*](OperatorsAA#*), [+](OperatorsAA#+), [as_4_grid](OperatorsAA#as_4_grid), [as_grid](OperatorsAA#as_grid), [as_hexagonal_grid](OperatorsAA#as_hexagonal_grid), [at_location](OperatorsAA#at_location), [clean](OperatorsBC#clean), [clean_network](OperatorsBC#clean_network), [convex_hull](OperatorsBC#convex_hull), [CRS_transform](OperatorsBC#crs_transform), [rotated_by](OperatorsNR#rotated_by), [scaled_to](OperatorsSZ#scaled_to), [simplification](OperatorsSZ#simplification), [skeletonize](OperatorsSZ#skeletonize), [smooth](OperatorsSZ#smooth), [split_geometry](OperatorsSZ#split_geometry), [split_lines](OperatorsSZ#split_lines), [to_GAMA_CRS](OperatorsSZ#to_gama_crs), [to_rectangles](OperatorsSZ#to_rectangles), [to_squares](OperatorsSZ#to_squares), [to_sub_geometries](OperatorsSZ#to_sub_geometries), [transformed_by](OperatorsSZ#transformed_by), [translated_by](OperatorsSZ#translated_by), [triangulate](OperatorsSZ#triangulate), [voronoi](OperatorsSZ#voronoi), [with_precision](OperatorsSZ#with_precision), [without_holes](OperatorsSZ#without_holes), 

----

### Species-related operators
[index_of](OperatorsIM#index_of), [last_index_of](OperatorsIM#last_index_of), [of_generic_species](OperatorsNR#of_generic_species), [of_species](OperatorsNR#of_species), 

----

### Statistical operators
[build](OperatorsBC#build), [corR](OperatorsBC#corr), [dbscan](OperatorsDH#dbscan), [distribution_of](OperatorsDH#distribution_of), [distribution2d_of](OperatorsDH#distribution2d_of), [dtw](OperatorsDH#dtw), [frequency_of](OperatorsDH#frequency_of), [gamma_rnd](OperatorsDH#gamma_rnd), [geometric_mean](OperatorsDH#geometric_mean), [gini](OperatorsDH#gini), [harmonic_mean](OperatorsDH#harmonic_mean), [hierarchical_clustering](OperatorsDH#hierarchical_clustering), [kmeans](OperatorsIM#kmeans), [kurtosis](OperatorsIM#kurtosis), [max](OperatorsIM#max), [mean](OperatorsIM#mean), [mean_deviation](OperatorsIM#mean_deviation), [meanR](OperatorsIM#meanr), [median](OperatorsIM#median), [min](OperatorsIM#min), [moran](OperatorsIM#moran), [mul](OperatorsIM#mul), [predict](OperatorsNR#predict), [simple_clustering_by_distance](OperatorsSZ#simple_clustering_by_distance), [skewness](OperatorsSZ#skewness), [split](OperatorsSZ#split), [split_in](OperatorsSZ#split_in), [split_using](OperatorsSZ#split_using), [standard_deviation](OperatorsSZ#standard_deviation), [sum](OperatorsSZ#sum), [variance](OperatorsSZ#variance), 

----

### Strings-related operators
[+](OperatorsAA#+), [<](OperatorsAA#<), [<=](OperatorsAA#<=), [>](OperatorsAA#>), [>=](OperatorsAA#>=), [at](OperatorsAA#at), [char](OperatorsBC#char), [contains](OperatorsBC#contains), [contains_all](OperatorsBC#contains_all), [contains_any](OperatorsBC#contains_any), [copy_between](OperatorsBC#copy_between), [date](OperatorsDH#date), [empty](OperatorsDH#empty), [first](OperatorsDH#first), [in](OperatorsIM#in), [indented_by](OperatorsIM#indented_by), [index_of](OperatorsIM#index_of), [is_number](OperatorsIM#is_number), [last](OperatorsIM#last), [last_index_of](OperatorsIM#last_index_of), [length](OperatorsIM#length), [lower_case](OperatorsIM#lower_case), [replace](OperatorsNR#replace), [replace_regex](OperatorsNR#replace_regex), [reverse](OperatorsNR#reverse), [sample](OperatorsSZ#sample), [shuffle](OperatorsSZ#shuffle), [split_with](OperatorsSZ#split_with), [string](OperatorsSZ#string), [upper_case](OperatorsSZ#upper_case), 

----

### System
[.](OperatorsAA#.), [command](OperatorsBC#command), [copy](OperatorsBC#copy), [dead](OperatorsDH#dead), [eval_gaml](OperatorsDH#eval_gaml), [every](OperatorsDH#every), [is_error](OperatorsIM#is_error), [is_warning](OperatorsIM#is_warning), [user_input](OperatorsSZ#user_input), 

----

### Time-related operators
[date](OperatorsDH#date), [string](OperatorsSZ#string), 

----

### Types-related operators


----

### User control operators
[user_input](OperatorsSZ#user_input), 
	
----

## Operators
	
    	
----

[//]: # (keyword|operator_BDIPlan)
### `BDIPlan`

#### Possible use: 
  *  **`BDIPlan`** (`any`) --->  `BDIPlan` 

#### Result: 
Casts the operand into the type BDIPlan
    	
----

[//]: # (keyword|operator_before)
### `before`

#### Possible use: 
  *  **`before`** (`date`) --->  `bool`
  * `any expression` **`before`** `date` --->  `bool`
  *  **`before`** (`any expression` , `date`) --->  `bool` 

#### Result: 
Returns true if the current_date of the model is strictly before the date passed in argument. Synonym of 'current_date < argument'

#### Examples: 
```
reflex when: before(starting_date) {} 	// this reflex will never be run 

```
  
    	
----

[//]: # (keyword|operator_beta)
### `beta`

#### Possible use: 
  * `float` **`beta`** `float` --->  `float`
  *  **`beta`** (`float` , `float`) --->  `float` 

#### Result: 
Returns the beta function with arguments a, b.
    	
----

[//]: # (keyword|operator_beta_index)
### `beta_index`

#### Possible use: 
  *  **`beta_index`** (`graph`) --->  `float` 

#### Result: 
returns the beta index of the graph (Measures the level of connectivity in a graph and is expressed by the relationship between the number of links (e) over the number of nodes (v) : beta = e/v.

#### Examples: 
```
graph graphEpidemio <- graph([]);  
float var1 <- beta_index(graphEpidemio); // var1 equals the beta index of the graph

```
      


#### See also: 

[alpha_index](OperatorsAA#alpha_index), [gamma_index](OperatorsDH#gamma_index), [nb_cycles](OperatorsNR#nb_cycles), [connectivity_index](OperatorsBC#connectivity_index), 
    	
----

[//]: # (keyword|operator_between)
### `between`

#### Possible use: 
  * `date` **`between`** `date` --->  `bool`
  *  **`between`** (`date` , `date`) --->  `bool`
  *  **`between`** (`any expression`, `date`, `date`) --->  `bool`
  *  **`between`** (`int`, `int`, `int`) --->  `bool`
  *  **`between`** (`date`, `date`, `date`) --->  `bool`
  *  **`between`** (`float`, `float`, `float`) --->  `bool` 

#### Result: 
returns true the first integer operand is bigger than the second integer operand and smaller than the third integer operand

returns true if the first float operand is bigger than the second float operand and smaller than the third float operand

#### Special cases:     
  * returns true if the first operand is between the two dates passed in arguments (both exclusive). The version with 2 arguments compares the current_date with the 2 others 
  
```
 
bool var0 <- (date('2016-01-01') between(date('2000-01-01'), date('2020-02-02'))); // var0 equals true// // will return true if the current_date of the model is in_between the 2 between(date('2000-01-01'), date('2020-02-02')) 
``` 

    
  * returns true if the first operand is between the two dates passed in arguments (both exclusive). Can be combined with 'every' to express a frequency between two dates 
  
```
 
bool var3 <- (date('2016-01-01') between(date('2000-01-01'), date('2020-02-02'))); // var3 equals true// will return true every new day between these two dates, taking the first one as the starting point every(#day between(date('2000-01-01'), date('2020-02-02')))  
``` 



#### Examples: 
```
 
bool var6 <- between(5, 1, 10); // var6 equals true 
bool var7 <- between(5.0, 1.0, 10.0); // var7 equals true

```
  
    	
----

[//]: # (keyword|operator_betweenness_centrality)
### `betweenness_centrality`

#### Possible use: 
  *  **`betweenness_centrality`** (`graph`) --->  `map` 

#### Result: 
returns a map containing for each vertex (key), its betweenness centrality (value): number of shortest paths passing through each vertex

#### Examples: 
```
graph graphEpidemio <- graph([]);  
map var1 <- betweenness_centrality(graphEpidemio); // var1 equals the betweenness centrality index of the graph

```
  
    	
----

[//]: # (keyword|operator_biggest_cliques_of)
### `biggest_cliques_of`

#### Possible use: 
  *  **`biggest_cliques_of`** (`graph`) --->  `list<list>` 

#### Result: 
returns the biggest cliques of a graph using the Bron-Kerbosch clique detection algorithm

#### Examples: 
```
graph my_graph <- graph([]);  
list<list> var1 <- biggest_cliques_of (my_graph); // var1 equals the list of the biggest cliques as list

```
      


#### See also: 

[maximal_cliques_of](OperatorsIM#maximal_cliques_of), 
    	
----

[//]: # (keyword|operator_binomial)
### `binomial`

#### Possible use: 
  * `int` **`binomial`** `float` --->  `int`
  *  **`binomial`** (`int` , `float`) --->  `int` 

#### Result: 
A value from a random variable following a binomial distribution. The operands represent the number of experiments n and the success probability p.  

#### Comment: 
The binomial distribution is the discrete probability distribution of the number of successes in a sequence of n independent yes/no experiments, each of which yields success with probability p, cf. Binomial distribution on Wikipedia.

#### Examples: 
```
 
int var0 <- binomial(15,0.6); // var0 equals a random positive integer

```
      


#### See also: 

[poisson](OperatorsNR#poisson), [gauss](OperatorsDH#gauss), 
    	
----

[//]: # (keyword|operator_binomial_coeff)
### `binomial_coeff`

#### Possible use: 
  * `int` **`binomial_coeff`** `int` --->  `float`
  *  **`binomial_coeff`** (`int` , `int`) --->  `float` 

#### Result: 
Returns n choose k as a double. Note the integerization of the double return value.
    	
----

[//]: # (keyword|operator_binomial_complemented)
### `binomial_complemented`

#### Possible use: 
  *  **`binomial_complemented`** (`int`, `int`, `float`) --->  `float` 

#### Result: 
Returns the sum of the terms k+1 through n of the Binomial probability density, where n is the number of trials and P is the probability of success in the range 0 to 1.
    	
----

[//]: # (keyword|operator_binomial_sum)
### `binomial_sum`

#### Possible use: 
  *  **`binomial_sum`** (`int`, `int`, `float`) --->  `float` 

#### Result: 
Returns the sum of the terms 0 through k of the Binomial probability density, where n is the number of trials and p is the probability of success in the range 0 to 1.
    	
----

[//]: # (keyword|operator_blend)
### `blend`

#### Possible use: 
  * `rgb` **`blend`** `rgb` --->  `rgb`
  *  **`blend`** (`rgb` , `rgb`) --->  `rgb`
  *  **`blend`** (`rgb`, `rgb`, `float`) --->  `rgb` 

#### Result: 
Blend two colors with an optional ratio (c1 `*` r + c2 `*` (1 - r)) between 0 and 1

#### Special cases:     
  * If the ratio is omitted, an even blend is done 
  
```
 
rgb var1 <- blend(#red, #blue); // var1 equals to a color very close to the purple
``` 



#### Examples: 
```
 
rgb var3 <- blend(#red, #blue, 0.3); // var3 equals to a color between the purple and the blue

```
      


#### See also: 

[rgb](OperatorsNR#rgb), [hsb](OperatorsDH#hsb), 
    	
----

[//]: # (keyword|operator_bool)
### `bool`

#### Possible use: 
  *  **`bool`** (`any`) --->  `bool` 

#### Result: 
Casts the operand into the type bool
    	
----

[//]: # (keyword|operator_box)
### `box`

#### Possible use: 
  *  **`box`** (`point`) --->  `geometry`
  *  **`box`** (`float`, `float`, `float`) --->  `geometry` 

#### Result: 
A box geometry which side sizes are given by the operands.  

#### Comment: 
the center of the box is by default the location of the current agent in which has been called this operator.the center of the box is by default the location of the current agent in which has been called this operator.

#### Special cases:     
  * returns nil if the operand is nil.    
  * returns nil if the operand is nil.

#### Examples: 
```
 
geometry var0 <- box(10, 5 , 5); // var0 equals a geometry as a rectangle with width = 10, height = 5 depth= 5. 
geometry var1 <- box({10, 5 , 5}); // var1 equals a geometry as a rectangle with width = 10, height = 5 depth= 5.

```
      


#### See also: 

[around](OperatorsAA#around), [circle](OperatorsBC#circle), [sphere](OperatorsSZ#sphere), [cone](OperatorsBC#cone), [line](OperatorsIM#line), [link](OperatorsIM#link), [norm](OperatorsNR#norm), [point](OperatorsNR#point), [polygon](OperatorsNR#polygon), [polyline](OperatorsNR#polyline), [square](OperatorsSZ#square), [cube](OperatorsBC#cube), [triangle](OperatorsSZ#triangle), 
    	
----

[//]: # (keyword|operator_brewer_colors)
### `brewer_colors`

#### Possible use: 
  *  **`brewer_colors`** (`string`) --->  `list<rgb>`
  * `string` **`brewer_colors`** `int` --->  `list<rgb>`
  *  **`brewer_colors`** (`string` , `int`) --->  `list<rgb>` 

#### Result: 
Build a list of colors of a given type (see website http://colorbrewer2.org/). The list of palettes can be obtained by calling brewer_palettes
Build a list of colors of a given type (see website http://colorbrewer2.org/) with a given number of classes

#### Examples: 
```
 
list<rgb> var0 <- list<rgb> colors <- brewer_colors("OrRd");; // var0 equals a list of 6 blue colors 
list<rgb> var1 <- list<rgb> colors <- brewer_colors("Pastel1", 5);; // var1 equals a list of 5 sequential colors in the palette named 'Pastel1'. The list of palettes can be obtained by calling brewer_palettes

```
      


#### See also: 

[brewer_palettes](OperatorsBC#brewer_palettes), 
    	
----

[//]: # (keyword|operator_brewer_palettes)
### `brewer_palettes`

#### Possible use: 
  *  **`brewer_palettes`** (`int`) --->  `list<string>`
  * `int` **`brewer_palettes`** `int` --->  `list<string>`
  *  **`brewer_palettes`** (`int` , `int`) --->  `list<string>` 

#### Result: 
returns the list a palette with a given min number of classes)
returns the list a palette with a given min number of classes and max number of classes)

#### Examples: 
```
 
list<string> var0 <- list<string> palettes <- brewer_palettes(3);; // var0 equals a list of palettes that are composed of a min of 3 colors 
list<string> var1 <- list<string> palettes <- brewer_palettes(5,10);; // var1 equals a list of palettes that are composed of a min of 5 colors and a max of 10 colors

```
      


#### See also: 

[brewer_colors](OperatorsBC#brewer_colors), 
    	
----

[//]: # (keyword|operator_buffer)
### `buffer`
   Same signification as [+](OperatorsAA#+)
    	
----

[//]: # (keyword|operator_build)
### `build`

#### Possible use: 
  *  **`build`** (`matrix<float>`) --->  `regression`
  * `matrix<float>` **`build`** `string` --->  `regression`
  *  **`build`** (`matrix<float>` , `string`) --->  `regression` 

#### Result: 
returns the regression build from the matrix data (a row = an instance, the last value of each line is the y value) while using the given ordinary least squares method. Usage: build(data)
returns the regression build from the matrix data (a row = an instance, the last value of each line is the y value) while using the given method ("GLS" or "OLS"). Usage: build(data,method)

#### Examples: 
```
matrix([[1,2,3,4],[2,3,4,2]]) build(matrix([[1,2,3,4],[2,3,4,2]]),"GLS") 

```
  
    	
----

[//]: # (keyword|operator_ceil)
### `ceil`

#### Possible use: 
  *  **`ceil`** (`float`) --->  `float` 

#### Result: 
Maps the operand to the smallest following integer, i.e. the smallest integer not less than x.

#### Examples: 
```
 
float var0 <- ceil(3); // var0 equals 3.0 
float var1 <- ceil(3.5); // var1 equals 4.0 
float var2 <- ceil(-4.7); // var2 equals -4.0

```
      


#### See also: 

[floor](OperatorsDH#floor), [round](OperatorsNR#round), 
    	
----

[//]: # (keyword|operator_centroid)
### `centroid`

#### Possible use: 
  *  **`centroid`** (`geometry`) --->  `point` 

#### Result: 
Centroid (weighted sum of the centroids of a decomposition of the area into triangles) of the operand-geometry. Can be different to the location of the geometry

#### Examples: 
```
 
point var0 <- centroid(world); // var0 equals the centroid of the square, for example : {50.0,50.0}.

```
      


#### See also: 

[any_location_in](OperatorsAA#any_location_in), [closest_points_with](OperatorsBC#closest_points_with), [farthest_point_to](OperatorsDH#farthest_point_to), [points_at](OperatorsNR#points_at), 
    	
----

[//]: # (keyword|operator_char)
### `char`

#### Possible use: 
  *  **`char`** (`int`) --->  `string`

#### Special cases:     
  * converts ACSII integer value to character 
  
```
 
string var0 <- char (34); // var0 equals '"'
``` 


    	
----

[//]: # (keyword|operator_chi_square)
### `chi_square`

#### Possible use: 
  * `float` **`chi_square`** `float` --->  `float`
  *  **`chi_square`** (`float` , `float`) --->  `float` 

#### Result: 
Returns the area under the left hand tail (from 0 to x) of the Chi square probability density function with df degrees of freedom.
    	
----

[//]: # (keyword|operator_chi_square_complemented)
### `chi_square_complemented`

#### Possible use: 
  * `float` **`chi_square_complemented`** `float` --->  `float`
  *  **`chi_square_complemented`** (`float` , `float`) --->  `float` 

#### Result: 
Returns the area under the right hand tail (from x to infinity) of the Chi square probability density function with df degrees of freedom.
    	
----

[//]: # (keyword|operator_circle)
### `circle`

#### Possible use: 
  *  **`circle`** (`float`) --->  `geometry`
  * `float` **`circle`** `point` --->  `geometry`
  *  **`circle`** (`float` , `point`) --->  `geometry` 

#### Result: 
A circle geometry which radius is equal to the first operand, and the center has the location equal to the second operand.
A circle geometry which radius is equal to the operand.  

#### Comment: 
the center of the circle is by default the location of the current agent in which has been called this operator.

#### Special cases:     
  * returns a point if the operand is lower or equal to 0.    
  * returns a point if the operand is lower or equal to 0.

#### Examples: 
```
 
geometry var0 <- circle(10,{80,30}); // var0 equals a geometry as a circle of radius 10, the center will be in the location {80,30}. 
geometry var1 <- circle(10); // var1 equals a geometry as a circle of radius 10.

```
      


#### See also: 

[around](OperatorsAA#around), [cone](OperatorsBC#cone), [line](OperatorsIM#line), [link](OperatorsIM#link), [norm](OperatorsNR#norm), [point](OperatorsNR#point), [polygon](OperatorsNR#polygon), [polyline](OperatorsNR#polyline), [rectangle](OperatorsNR#rectangle), [square](OperatorsSZ#square), [triangle](OperatorsSZ#triangle), 
    	
----

[//]: # (keyword|operator_clean)
### `clean`

#### Possible use: 
  *  **`clean`** (`geometry`) --->  `geometry` 

#### Result: 
A geometry corresponding to the cleaning of the operand (geometry, agent, point)  

#### Comment: 
The cleaning corresponds to a buffer with a distance of 0.0

#### Examples: 
```
 
geometry var0 <- clean(self); // var0 equals returns the geometry resulting from the cleaning of the geometry of the agent applying the operator.

```
  
    	
----

[//]: # (keyword|operator_clean_network)
### `clean_network`

#### Possible use: 
  *  **`clean_network`** (`list<geometry>`, `float`, `bool`, `bool`) --->  `list<geometry>` 

#### Result: 
A list of polylines corresponding to the cleaning of the first operand (list of polyline geometry or agents), considering the tolerance distance given by the second operand; the third operator is used to define if the operator should as well split the lines at their intersections(true to split the lines); the last operandis used to specify if the operator should as well keep only the main connected component of the network. Usage: clean_network(lines:list of geometries or agents, tolerance: float, split_lines: bool, keepMainConnectedComponent: bool)  

#### Comment: 
The cleaned set of polylines

#### Examples: 
```
 
list<geometry> var0 <- clean_network(my_road_shapefile.contents, 1.0, true, false); // var0 equals returns the list of polulines resulting from the cleaning of the geometry of the agent applying the operator with a tolerance of 1m, and splitting the lines at their intersections.

```
  
    	
----

[//]: # (keyword|operator_closest_points_with)
### `closest_points_with`

#### Possible use: 
  * `geometry` **`closest_points_with`** `geometry` --->  `list<point>`
  *  **`closest_points_with`** (`geometry` , `geometry`) --->  `list<point>` 

#### Result: 
A list of two closest points between the two geometries.

#### Examples: 
```
 
list<point> var0 <- geom1 closest_points_with(geom2); // var0 equals [pt1, pt2] with pt1 the closest point of geom1 to geom2 and pt1 the closest point of geom2 to geom1

```
      


#### See also: 

[any_location_in](OperatorsAA#any_location_in), [any_point_in](OperatorsAA#any_point_in), [farthest_point_to](OperatorsDH#farthest_point_to), [points_at](OperatorsNR#points_at), 
    	
----

[//]: # (keyword|operator_closest_to)
### `closest_to`

#### Possible use: 
  * `container<agent>` **`closest_to`** `geometry` --->  `geometry`
  *  **`closest_to`** (`container<agent>` , `geometry`) --->  `geometry`
  *  **`closest_to`** (`container<agent>`, `geometry`, `int`) --->  `list<geometry>` 

#### Result: 
An agent or a geometry among the left-operand list of agents, species or meta-population (addition of species), the closest to the operand (casted as a geometry).
The N agents or geometries among the left-operand list of agents, species or meta-population (addition of species), that are the closest to the operand (casted as a geometry).  

#### Comment: 
the distance is computed in the topology of the calling agent (the agent in which this operator is used), with the distance algorithm specific to the topology.the distance is computed in the topology of the calling agent (the agent in which this operator is used), with the distance algorithm specific to the topology.

#### Examples: 
```
 
geometry var0 <- [ag1, ag2, ag3] closest_to(self); // var0 equals return the closest agent among ag1, ag2 and ag3 to the agent applying the operator.(species1 + species2) closest_to self  
list<geometry> var2 <- [ag1, ag2, ag3] closest_to(self, 2); // var2 equals return the 2 closest agents among ag1, ag2 and ag3 to the agent applying the operator.(species1 + species2) closest_to (self, 5) 

```
      


#### See also: 

[neighbors_at](OperatorsNR#neighbors_at), [neighbors_of](OperatorsNR#neighbors_of), [inside](OperatorsIM#inside), [overlapping](OperatorsNR#overlapping), [agents_overlapping](OperatorsAA#agents_overlapping), [agents_inside](OperatorsAA#agents_inside), [agent_closest_to](OperatorsAA#agent_closest_to), 
    	
----

[//]: # (keyword|operator_collect)
### `collect`

#### Possible use: 
  * `container` **`collect`** `any expression` --->  `list`
  *  **`collect`** (`container` , `any expression`) --->  `list` 

#### Result: 
returns a new list, in which each element is the evaluation of the right-hand operand.  

#### Comment: 
collect is similar to accumulate except that accumulate always produces flat lists if the right-hand operand returns a list.In addition, collect can be applied to any container.

#### Special cases:     
  * if the left-hand operand is nil, collect throws an error

#### Examples: 
```
 
list var0 <- [1,2,4] collect (each *2); // var0 equals [2,4,8] 
list var1 <- [1,2,4] collect ([2,4]); // var1 equals [[2,4],[2,4],[2,4]] 
list var2 <- [1::2, 3::4, 5::6] collect (each + 2); // var2 equals [4,6,8] 
list var3 <- (list(node) collect (node(each).location.x * 2); // var3 equals the list of nodes with their x multiplied by 2

```
      


#### See also: 

[accumulate](OperatorsAA#accumulate), 
    	
----

[//]: # (keyword|operator_column_at)
### `column_at`

#### Possible use: 
  * `matrix` **`column_at`** `int` --->  `list`
  *  **`column_at`** (`matrix` , `int`) --->  `list` 

#### Result: 
returns the column at a num_col (right-hand operand)

#### Examples: 
```
 
list var0 <- matrix([["el11","el12","el13"],["el21","el22","el23"],["el31","el32","el33"]]) column_at 2; // var0 equals ["el31","el32","el33"]

```
      


#### See also: 

[row_at](OperatorsNR#row_at), [rows_list](OperatorsNR#rows_list), 
    	
----

[//]: # (keyword|operator_columns_list)
### `columns_list`

#### Possible use: 
  *  **`columns_list`** (`matrix`) --->  `list<list>` 

#### Result: 
returns a list of the columns of the matrix, with each column as a list of elements

#### Examples: 
```
 
list<list> var0 <- columns_list(matrix([["el11","el12","el13"],["el21","el22","el23"],["el31","el32","el33"]])); // var0 equals [["el11","el12","el13"],["el21","el22","el23"],["el31","el32","el33"]]

```
      


#### See also: 

[rows_list](OperatorsNR#rows_list), 
    	
----

[//]: # (keyword|operator_command)
### `command`

#### Possible use: 
  *  **`command`** (`string`) --->  `string`
  * `string` **`command`** `string` --->  `string`
  *  **`command`** (`string` , `string`) --->  `string`
  *  **`command`** (`string`, `string`, `msi.gama.util.GamaMap<java.lang.String,java.lang.String>`) --->  `string` 

#### Result: 
command allows GAMA to issue a system command using the system terminal or shell and to receive a string containing the outcome of the command or script executed. By default, commands are blocking the agent calling them, unless the sequence ' &' is used at the end. In this case, the result of the operator is an empty string
command allows GAMA to issue a system command using the system terminal or shell and to receive a string containing the outcome of the command or script executed. By default, commands are blocking the agent calling them, unless the sequence ' &' is used at the end. In this case, the result of the operator is an empty string. The basic form with only one string in argument uses the directory of the model and does not set any environment variables. Two other forms (with a directory and a map<string, string> of environment variables) are available.
command allows GAMA to issue a system command using the system terminal or shell and to receive a string containing the outcome of the command or script executed. By default, commands are blocking the agent calling them, unless the sequence ' &' is used at the end. In this case, the result of the operator is an empty string. The basic form with only one string in argument uses the directory of the model and does not set any environment variables. Two other forms (with a directory and a map<string, string> of environment variables) are available.
    	
----

[//]: # (keyword|operator_cone)
### `cone`

#### Possible use: 
  *  **`cone`** (`point`) --->  `geometry`
  * `int` **`cone`** `int` --->  `geometry`
  *  **`cone`** (`int` , `int`) --->  `geometry` 

#### Result: 
A cone geometry which min and max angles are given by the operands.
A cone geometry which min and max angles are given by the operands.  

#### Comment: 
the center of the cone is by default the location of the current agent in which has been called this operator.the center of the cone is by default the location of the current agent in which has been called this operator.

#### Special cases:     
  * returns nil if the operand is nil.    
  * returns nil if the operand is nil.

#### Examples: 
```
 
geometry var0 <- cone(0, 45); // var0 equals a geometry as a cone with min angle is 0 and max angle is 45. 
geometry var1 <- cone({0, 45}); // var1 equals a geometry as a cone with min angle is 0 and max angle is 45.

```
      


#### See also: 

[around](OperatorsAA#around), [circle](OperatorsBC#circle), [line](OperatorsIM#line), [link](OperatorsIM#link), [norm](OperatorsNR#norm), [point](OperatorsNR#point), [polygon](OperatorsNR#polygon), [polyline](OperatorsNR#polyline), [rectangle](OperatorsNR#rectangle), [square](OperatorsSZ#square), [triangle](OperatorsSZ#triangle), 
    	
----

[//]: # (keyword|operator_cone3D)
### `cone3D`

#### Possible use: 
  * `float` **`cone3D`** `float` --->  `geometry`
  *  **`cone3D`** (`float` , `float`) --->  `geometry` 

#### Result: 
A cone geometry which base radius size is equal to the first operand, and which the height is equal to the second operand.  

#### Comment: 
the center of the cone is by default the location of the current agent in which has been called this operator.

#### Special cases:     
  * returns a point if the operand is lower or equal to 0.

#### Examples: 
```
 
geometry var0 <- cone3D(10.0,5.0); // var0 equals a geometry as a cone with a base circle of radius 10 and a height of 5.

```
      


#### See also: 

[around](OperatorsAA#around), [cone](OperatorsBC#cone), [line](OperatorsIM#line), [link](OperatorsIM#link), [norm](OperatorsNR#norm), [point](OperatorsNR#point), [polygon](OperatorsNR#polygon), [polyline](OperatorsNR#polyline), [rectangle](OperatorsNR#rectangle), [square](OperatorsSZ#square), [triangle](OperatorsSZ#triangle), 
    	
----

[//]: # (keyword|operator_connected_components_of)
### `connected_components_of`

#### Possible use: 
  *  **`connected_components_of`** (`graph`) --->  `list<list>`
  * `graph` **`connected_components_of`** `bool` --->  `list<list>`
  *  **`connected_components_of`** (`graph` , `bool`) --->  `list<list>` 

#### Result: 
returns the connected components of a graph, i.e. the list of all vertices that are in the maximally connected component together with the specified vertex. 
returns the connected components of a graph, i.e. the list of all edges (if the boolean is true) or vertices (if the boolean is false) that are in the connected components.

#### Examples: 
```
graph my_graph <- graph([]);  
list<list> var1 <- connected_components_of (my_graph); // var1 equals the list of all the components as listgraph my_graph2 <- graph([]);  
list<list> var3 <- connected_components_of (my_graph2, true); // var3 equals the list of all the components as list

```
      


#### See also: 

[alpha_index](OperatorsAA#alpha_index), [connectivity_index](OperatorsBC#connectivity_index), [nb_cycles](OperatorsNR#nb_cycles), 
    	
----

[//]: # (keyword|operator_connectivity_index)
### `connectivity_index`

#### Possible use: 
  *  **`connectivity_index`** (`graph`) --->  `float` 

#### Result: 
returns a simple connectivity index. This number is estimated through the number of nodes (v) and of sub-graphs (p) : IC = (v - p) /(v - 1).

#### Examples: 
```
graph graphEpidemio <- graph([]);  
float var1 <- connectivity_index(graphEpidemio); // var1 equals the connectivity index of the graph

```
      


#### See also: 

[alpha_index](OperatorsAA#alpha_index), [beta_index](OperatorsBC#beta_index), [gamma_index](OperatorsDH#gamma_index), [nb_cycles](OperatorsNR#nb_cycles), 
    	
----

[//]: # (keyword|operator_container)
### `container`

#### Possible use: 
  *  **`container`** (`any`) --->  `container` 

#### Result: 
Casts the operand into the type container
    	
----

[//]: # (keyword|operator_contains)
### `contains`

#### Possible use: 
  * `container<KeyType,ValueType>` **`contains`** `unknown` --->  `bool`
  *  **`contains`** (`container<KeyType,ValueType>` , `unknown`) --->  `bool`
  * `string` **`contains`** `string` --->  `bool`
  *  **`contains`** (`string` , `string`) --->  `bool` 

#### Result: 
true, if the container contains the right operand, false otherwise  

#### Comment: 
the contains operator behavior depends on the nature of the operand

#### Special cases:     
  * if it is a map, contains returns true if the operand is a key of the map    
  * if it is a file, contains returns true it the operand is contained in the file content    
  * if it is a population, contains returns true if the operand is an agent of the population, false otherwise    
  * if it is a graph, contains returns true if the operand is a node or an edge of the graph, false otherwise    
  * if both operands are strings, returns true if the right-hand operand contains the right-hand pattern;    
  * if it is a list or a matrix, contains returns true if the list or matrix contains the right operand 
  
```
 
bool var0 <- [1, 2, 3] contains 2; // var0 equals true 
bool var1 <- [{1,2}, {3,4}, {5,6}] contains {3,4}; // var1 equals true
``` 



#### Examples: 
```
 
bool var2 <- 'abcded' contains 'bc'; // var2 equals true

```
      


#### See also: 

[contains_all](OperatorsBC#contains_all), [contains_any](OperatorsBC#contains_any), 
    	
----

[//]: # (keyword|operator_contains_all)
### `contains_all`

#### Possible use: 
  * `string` **`contains_all`** `list` --->  `bool`
  *  **`contains_all`** (`string` , `list`) --->  `bool`
  * `container` **`contains_all`** `container` --->  `bool`
  *  **`contains_all`** (`container` , `container`) --->  `bool` 

#### Result: 
true if the left operand contains all the elements of the right operand, false otherwise  

#### Comment: 
the definition of contains depends on the container

#### Special cases:     
  * if the right operand is nil or empty, contains_all returns true    
  * if the left-operand is a string, test whether the string contains all the element of the list; 
  
```
 
bool var0 <- "abcabcabc" contains_all ["ca","xy"]; // var0 equals false
``` 



#### Examples: 
```
 
bool var1 <- [1,2,3,4,5,6] contains_all [2,4]; // var1 equals true  
bool var2 <- [1,2,3,4,5,6] contains_all [2,8]; // var2 equals false 
bool var3 <- [1::2, 3::4, 5::6] contains_all [1,3]; // var3 equals false  
bool var4 <- [1::2, 3::4, 5::6] contains_all [2,4]; // var4 equals true

```
      


#### See also: 

[contains](OperatorsBC#contains), [contains_any](OperatorsBC#contains_any), 
    	
----

[//]: # (keyword|operator_contains_any)
### `contains_any`

#### Possible use: 
  * `string` **`contains_any`** `list` --->  `bool`
  *  **`contains_any`** (`string` , `list`) --->  `bool`
  * `container` **`contains_any`** `container` --->  `bool`
  *  **`contains_any`** (`container` , `container`) --->  `bool` 

#### Result: 
true if the left operand contains one of the elements of the right operand, false otherwise  

#### Comment: 
the definition of contains depends on the container

#### Special cases:     
  * if the right operand is nil or empty, contains_any returns false

#### Examples: 
```
 
bool var0 <- "abcabcabc" contains_any ["ca","xy"]; // var0 equals true 
bool var1 <- [1,2,3,4,5,6] contains_any [2,4]; // var1 equals true  
bool var2 <- [1,2,3,4,5,6] contains_any [2,8]; // var2 equals true 
bool var3 <- [1::2, 3::4, 5::6] contains_any [1,3]; // var3 equals false 
bool var4 <- [1::2, 3::4, 5::6] contains_any [2,4]; // var4 equals true

```
      


#### See also: 

[contains](OperatorsBC#contains), [contains_all](OperatorsBC#contains_all), 
    	
----

[//]: # (keyword|operator_contains_edge)
### `contains_edge`

#### Possible use: 
  * `graph` **`contains_edge`** `unknown` --->  `bool`
  *  **`contains_edge`** (`graph` , `unknown`) --->  `bool`
  * `graph` **`contains_edge`** `pair` --->  `bool`
  *  **`contains_edge`** (`graph` , `pair`) --->  `bool` 

#### Result: 
returns true if the graph(left-hand operand) contains the given edge (righ-hand operand), false otherwise

#### Special cases:     
  * if the left-hand operand is nil, returns false    
  * if the right-hand operand is a pair, returns true if it exists an edge between the two elements of the pair in the graph 
  
```
 
bool var2 <- graphEpidemio contains_edge (node(0)::node(3)); // var2 equals true
``` 



#### Examples: 
```
graph graphFromMap <-  as_edge_graph([{1,5}::{12,45},{12,45}::{34,56}]);  
bool var1 <- graphFromMap contains_edge link({1,5},{12,45}); // var1 equals true

```
      


#### See also: 

[contains_vertex](OperatorsBC#contains_vertex), 
    	
----

[//]: # (keyword|operator_contains_vertex)
### `contains_vertex`

#### Possible use: 
  * `graph` **`contains_vertex`** `unknown` --->  `bool`
  *  **`contains_vertex`** (`graph` , `unknown`) --->  `bool` 

#### Result: 
returns true if the graph(left-hand operand) contains the given vertex (righ-hand operand), false otherwise

#### Special cases:     
  * if the left-hand operand is nil, returns false

#### Examples: 
```
graph graphFromMap<-  as_edge_graph([{1,5}::{12,45},{12,45}::{34,56}]);  
bool var1 <- graphFromMap contains_vertex {1,5}; // var1 equals true

```
      


#### See also: 

[contains_edge](OperatorsBC#contains_edge), 
    	
----

[//]: # (keyword|operator_conversation)
### `conversation`

#### Possible use: 
  *  **`conversation`** (`unknown`) --->  `conversation`
    	
----

[//]: # (keyword|operator_convex_hull)
### `convex_hull`

#### Possible use: 
  *  **`convex_hull`** (`geometry`) --->  `geometry` 

#### Result: 
A geometry corresponding to the convex hull of the operand.

#### Examples: 
```
 
geometry var0 <- convex_hull(self); // var0 equals the convex hull of the geometry of the agent applying the operator

```
  
    	
----

[//]: # (keyword|operator_copy)
### `copy`

#### Possible use: 
  *  **`copy`** (`unknown`) --->  `unknown` 

#### Result: 
returns a copy of the operand.
    	
----

[//]: # (keyword|operator_copy_between)
### `copy_between`

#### Possible use: 
  *  **`copy_between`** (`string`, `int`, `int`) --->  `string`
  *  **`copy_between`** (`list`, `int`, `int`) --->  `list` 

#### Result: 
Returns a copy of the first operand between the indexes determined by the second (inclusive) and third operands (exclusive)

#### Special cases:     
  * If the first operand is empty, returns an empty object of the same type    
  * If the second operand is greater than or equal to the third operand, return an empty object of the same type    
  * If the first operand is nil, raises an error

#### Examples: 
```
 
string var0 <- copy_between("abcabcabc", 2,6); // var0 equals "cabc" 
list var1 <-  copy_between ([4, 1, 6, 9 ,7], 1, 3); // var1 equals [1, 6]

```
  
    	
----

[//]: # (keyword|operator_corR)
### `corR`

#### Possible use: 
  * `container` **`corR`** `container` --->  `unknown`
  *  **`corR`** (`container` , `container`) --->  `unknown` 

#### Result: 
returns the Pearson correlation coefficient of two given vectors (right-hand operands) in given variable  (left-hand operand).

#### Special cases:     
  * if the lengths of two vectors in the right-hand aren't equal, returns 0

#### Examples: 
```
list X <- [1, 2, 3]; list Y <- [1, 2, 4];  
unknown var2 <- corR(X, Y); // var2 equals 0.981980506061966

```
  
    	
----

[//]: # (keyword|operator_correlation)
### `correlation`

#### Possible use: 
  * `container` **`correlation`** `container` --->  `float`
  *  **`correlation`** (`container` , `container`) --->  `float` 

#### Result: 
Returns the correlation of two data sequences
    	
----

[//]: # (keyword|operator_cos)
### `cos`

#### Possible use: 
  *  **`cos`** (`int`) --->  `float`
  *  **`cos`** (`float`) --->  `float` 

#### Result: 
Returns the value (in [-1,1]) of the cosinus of the operand (in decimal degrees).  The argument is casted to an int before being evaluated.

#### Special cases:     
  * Operand values out of the range [0-359] are normalized.

#### Examples: 
```
 
float var0 <- cos (0); // var0 equals 1.0 
float var1 <- cos(360); // var1 equals 1.0 
float var2 <- cos(-720); // var2 equals 1.0

```
      


#### See also: 

[sin](OperatorsSZ#sin), [tan](OperatorsSZ#tan), 
    	
----

[//]: # (keyword|operator_cos_rad)
### `cos_rad`

#### Possible use: 
  *  **`cos_rad`** (`float`) --->  `float` 

#### Result: 
Returns the value (in [-1,1]) of the cosinus of the operand (in radians).

#### Special cases:     
  * Operand values out of the range [0-359] are normalized.    


#### See also: 

[sin](OperatorsSZ#sin), [tan](OperatorsSZ#tan), 
    	
----

[//]: # (keyword|operator_count)
### `count`

#### Possible use: 
  * `container` **`count`** `any expression` --->  `int`
  *  **`count`** (`container` , `any expression`) --->  `int` 

#### Result: 
returns an int, equal to the number of elements of the left-hand operand that make the right-hand operand evaluate to true.  

#### Comment: 
in the right-hand operand, the keyword each can be used to represent, in turn, each of the elements.

#### Special cases:     
  * if the left-hand operand is nil, count throws an error

#### Examples: 
```
 
int var0 <- [1,2,3,4,5,6,7,8] count (each > 3); // var0 equals 5// Number of nodes of graph g2 without any out edge graph g2 <- graph([]);  
int var3 <- g2 count (length(g2 out_edges_of each) = 0  ) ; // var3 equals the total number of out edges// Number of agents node with x > 32 int n <- (list(node) count (round(node(each).location.x) > 32);  
int var6 <- [1::2, 3::4, 5::6] count (each > 4); // var6 equals 1

```
      


#### See also: 

[group_by](OperatorsDH#group_by), 
    	
----

[//]: # (keyword|operator_covariance)
### `covariance`

#### Possible use: 
  * `container` **`covariance`** `container` --->  `float`
  *  **`covariance`** (`container` , `container`) --->  `float` 

#### Result: 
Returns the covariance of two data sequences
    	
----

[//]: # (keyword|operator_covers)
### `covers`

#### Possible use: 
  * `geometry` **`covers`** `geometry` --->  `bool`
  *  **`covers`** (`geometry` , `geometry`) --->  `bool` 

#### Result: 
A boolean, equal to true if the left-geometry (or agent/point) covers the right-geometry (or agent/point).

#### Special cases:     
  * if one of the operand is null, returns false.

#### Examples: 
```
 
bool var0 <- square(5) covers square(2); // var0 equals true

```
      


#### See also: 

[disjoint_from](OperatorsDH#disjoint_from), [crosses](OperatorsBC#crosses), [overlaps](OperatorsNR#overlaps), [partially_overlaps](OperatorsNR#partially_overlaps), [touches](OperatorsSZ#touches), 
    	
----

[//]: # (keyword|operator_create_map)
### `create_map`

#### Possible use: 
  * `list` **`create_map`** `list` --->  `map`
  *  **`create_map`** (`list` , `list`) --->  `map` 

#### Result: 
returns a new map using the left operand as keys for the right operand

#### Special cases:     
  * if the left operand contains duplicates, create_map throws an error.    
  * if both operands have different lengths, choose the minimum length between the two operandsfor the size of the map

#### Examples: 
```
 
map<int,string> var0 <- create_map([0,1,2],['a','b','c']); // var0 equals [0::'a',1::'b',2::'c'] 
map<int,float> var1 <- create_map([0,1],[0.1,0.2,0.3]); // var1 equals [0::0.1,1::0.2] 
map<string,float> var2 <- create_map(['a','b','c','d'],[1.0,2.0,3.0]); // var2 equals ['a'::1.0,'b'::2.0,'c'::3.0]

```
  
    	
----

[//]: # (keyword|operator_cross)
### `cross`

#### Possible use: 
  *  **`cross`** (`float`) --->  `geometry`
  * `float` **`cross`** `float` --->  `geometry`
  *  **`cross`** (`float` , `float`) --->  `geometry` 

#### Result: 
A cross, which radius is equal to the first operand
A cross, which radius is equal to the first operand and the width of the lines for the second

#### Examples: 
```
 
geometry var0 <- cross(10); // var0 equals a geometry as a cross of radius 10 
geometry var1 <- cross(10,2); // var1 equals a geometry as a cross of radius 10, and with a width of 2 for the lines 

```
      


#### See also: 

[around](OperatorsAA#around), [cone](OperatorsBC#cone), [line](OperatorsIM#line), [link](OperatorsIM#link), [norm](OperatorsNR#norm), [point](OperatorsNR#point), [polygon](OperatorsNR#polygon), [polyline](OperatorsNR#polyline), [super_ellipse](OperatorsSZ#super_ellipse), [rectangle](OperatorsNR#rectangle), [square](OperatorsSZ#square), [circle](OperatorsBC#circle), [ellipse](OperatorsDH#ellipse), [triangle](OperatorsSZ#triangle), 
    	
----

[//]: # (keyword|operator_crosses)
### `crosses`

#### Possible use: 
  * `geometry` **`crosses`** `geometry` --->  `bool`
  *  **`crosses`** (`geometry` , `geometry`) --->  `bool` 

#### Result: 
A boolean, equal to true if the left-geometry (or agent/point) crosses the right-geometry (or agent/point).

#### Special cases:     
  * if one of the operand is null, returns false.    
  * if one operand is a point, returns false.

#### Examples: 
```
 
bool var0 <- polyline([{10,10},{20,20}]) crosses polyline([{10,20},{20,10}]); // var0 equals true 
bool var1 <- polyline([{10,10},{20,20}]) crosses {15,15}; // var1 equals true 
bool var2 <- polyline([{0,0},{25,25}]) crosses polygon([{10,10},{10,20},{20,20},{20,10}]); // var2 equals true

```
      


#### See also: 

[disjoint_from](OperatorsDH#disjoint_from), [intersects](OperatorsIM#intersects), [overlaps](OperatorsNR#overlaps), [partially_overlaps](OperatorsNR#partially_overlaps), [touches](OperatorsSZ#touches), 
    	
----

[//]: # (keyword|operator_crs)
### `crs`

#### Possible use: 
  *  **`crs`** (`file`) --->  `string` 

#### Result: 
the Coordinate Reference System (CRS) of the GIS file

#### Examples: 
```
 
string var0 <- crs(my_shapefile); // var0 equals the crs of the shapefile

```
  
    	
----

[//]: # (keyword|operator_CRS_transform)
### `CRS_transform`

#### Possible use: 
  *  **`CRS_transform`** (`geometry`) --->  `geometry`
  * `geometry` **`CRS_transform`** `string` --->  `geometry`
  *  **`CRS_transform`** (`geometry` , `string`) --->  `geometry`

#### Special cases:     
  * returns the geometry corresponding to the transformation of the given geometry by the left operand CRS (Coordinate Reference System) 
  
```
 
geometry var0 <- shape CRS_transform("EPSG:4326"); // var0 equals a geometry corresponding to the agent geometry transformed into the EPSG:4326 CRS
``` 

    
  * returns the geometry corresponding to the transformation of the given geometry by the current CRS (Coordinate Reference System), the one corresponding to the world's agent one 
  
```
 
geometry var1 <- CRS_transform(shape); // var1 equals a geometry corresponding to the agent geometry transformed into the current CRS
``` 


    	
----

[//]: # (keyword|operator_csv_file)
### `csv_file`

#### Possible use: 
  *  **`csv_file`** (`string`) --->  `file` 

#### Result: 
Constructs a file of type csv. Allowed extensions are limited to csv, tsv
    	
----

[//]: # (keyword|operator_cube)
### `cube`

#### Possible use: 
  *  **`cube`** (`float`) --->  `geometry` 

#### Result: 
A cube geometry which side size is equal to the operand.  

#### Comment: 
the center of the cube is by default the location of the current agent in which has been called this operator.

#### Special cases:     
  * returns nil if the operand is nil.

#### Examples: 
```
 
geometry var0 <- cube(10); // var0 equals a geometry as a square of side size 10.

```
      


#### See also: 

[around](OperatorsAA#around), [circle](OperatorsBC#circle), [cone](OperatorsBC#cone), [line](OperatorsIM#line), [link](OperatorsIM#link), [norm](OperatorsNR#norm), [point](OperatorsNR#point), [polygon](OperatorsNR#polygon), [polyline](OperatorsNR#polyline), [rectangle](OperatorsNR#rectangle), [triangle](OperatorsSZ#triangle), 
    	
----

[//]: # (keyword|operator_curve)
### `curve`

#### Possible use: 
  *  **`curve`** (`point`, `point`, `point`) --->  `geometry`
  *  **`curve`** (`point`, `point`, `float`) --->  `geometry`
  *  **`curve`** (`point`, `point`, `point`, `int`) --->  `geometry`
  *  **`curve`** (`point`, `point`, `float`, `float`) --->  `geometry`
  *  **`curve`** (`point`, `point`, `float`, `bool`) --->  `geometry`
  *  **`curve`** (`point`, `point`, `point`, `point`) --->  `geometry`
  *  **`curve`** (`point`, `point`, `float`, `bool`, `int`) --->  `geometry`
  *  **`curve`** (`point`, `point`, `point`, `point`, `int`) --->  `geometry`
  *  **`curve`** (`point`, `point`, `float`, `int`, `float`) --->  `geometry`
  *  **`curve`** (`point`, `point`, `float`, `int`, `float`, `float`) --->  `geometry`
  *  **`curve`** (`point`, `point`, `float`, `bool`, `int`, `float`) --->  `geometry` 

#### Result: 
A cubic Bezier curve geometry built from the two given points with the given coefficient for the radius and composed of the given number of points, considering the given inflection point (between 0.0 and 1.0 - default 0.5), and the given rotation angle (90 = along the z axis).
A quadratic Bezier curve geometry built from the three given points composed of a given numnber of points.
A cubic Bezier curve geometry built from the two given points with the given coefficient for the radius considering the given rotation angle (90 = along the z axis).
A cubic Bezier curve geometry built from the two given points with the given coefficient for the radius and composed of the given number of points - the boolean is used to specified if it is the right side.
A quadratic Bezier curve geometry built from the three given points composed of 10 points.
A cubic Bezier curve geometry built from the four given points composed of a given number of points.
A cubic Bezier curve geometry built from the two given points with the given coefficient for the radius and composed of the given number of points, considering the given rotation angle (90 = along the z axis).
A cubic Bezier curve geometry built from the two given points with the given coefficient for the radius and composed of 10 points - the last boolean is used to specified if it is the right side.
A cubic Bezier curve geometry built from the two given points with the given coefficient for the radius and composed of the given number of points - the boolean is used to specified if it is the right side and the last value to indicate where is the inflection point (between 0.0 and 1.0 - default 0.5).
A cubic Bezier curve geometry built from the two given points with the given coefficient for the radius and composed of 10 points.
A cubic Bezier curve geometry built from the four given points composed of 10 points.

#### Special cases:     
  * if the operand is nil, returns nil    
  * if the operand is nil, returns nil    
  * if the last operand (number of points) is inferior to 2, returns nil    
  * if the operand is nil, returns nil    
  * if the operand is nil, returns nil    
  * if the operand is nil, returns nil    
  * if the operand is nil, returns nil    
  * if the last operand (number of points) is inferior to 2, returns nil    
  * if the operand is nil, returns nil    
  * if the operand is nil, returns nil    
  * if the operand is nil, returns nil    
  * if the operand is nil, returns nil    
  * if the operand is nil, returns nil

#### Examples: 
```
 
geometry var0 <- curve({0,0},{10,10}, 0.5, 100, 0.8, 90); // var0 equals a cubic Bezier curve geometry composed of 100 points from p0 to p1 at the right side. 
geometry var1 <- curve({0,0}, {0,10}, {10,10}, 20); // var1 equals a quadratic Bezier curve geometry composed of 20 points from p0 to p2. 
geometry var2 <- curve({0,0},{10,10}, 0.5, 90); // var2 equals a cubic Bezier curve geometry composed of 100 points from p0 to p1 at the right side. 
geometry var3 <- curve({0,0},{10,10}, 0.5, false, 100); // var3 equals a cubic Bezier curve geometry composed of 100 points from p0 to p1 at the right side. 
geometry var4 <- curve({0,0}, {0,10}, {10,10}); // var4 equals a quadratic Bezier curve geometry composed of 10 points from p0 to p2. 
geometry var5 <- curve({0,0}, {0,10}, {10,10}); // var5 equals a cubic Bezier curve geometry composed of 10 points from p0 to p3. 
geometry var6 <- curve({0,0},{10,10}, 0.5, 100, 90); // var6 equals a cubic Bezier curve geometry composed of 100 points from p0 to p1 at the right side. 
geometry var7 <- curve({0,0},{10,10}, 0.5, false); // var7 equals a cubic Bezier curve geometry composed of 10 points from p0 to p1 at the left side. 
geometry var8 <- curve({0,0},{10,10}, 0.5, false, 100, 0.8); // var8 equals a cubic Bezier curve geometry composed of 100 points from p0 to p1 at the right side. 
geometry var9 <- curve({0,0},{10,10}, 0.5); // var9 equals a cubic Bezier curve geometry composed of 10 points from p0 to p1. 
geometry var10 <- curve({0,0}, {0,10}, {10,10}); // var10 equals a cubic Bezier curve geometry composed of 10 points from p0 to p3.

```
      


#### See also: 

[around](OperatorsAA#around), [circle](OperatorsBC#circle), [cone](OperatorsBC#cone), [link](OperatorsIM#link), [norm](OperatorsNR#norm), [point](OperatorsNR#point), [polygone](OperatorsSZ#polygone), [rectangle](OperatorsNR#rectangle), [square](OperatorsSZ#square), [triangle](OperatorsSZ#triangle), [line](OperatorsIM#line), 
    	
----

[//]: # (keyword|operator_cylinder)
### `cylinder`

#### Possible use: 
  * `float` **`cylinder`** `float` --->  `geometry`
  *  **`cylinder`** (`float` , `float`) --->  `geometry` 

#### Result: 
A cylinder geometry which radius is equal to the operand.  

#### Comment: 
the center of the cylinder is by default the location of the current agent in which has been called this operator.

#### Special cases:     
  * returns a point if the operand is lower or equal to 0.

#### Examples: 
```
 
geometry var0 <- cylinder(10,10); // var0 equals a geometry as a circle of radius 10.

```
      


#### See also: 

[around](OperatorsAA#around), [cone](OperatorsBC#cone), [line](OperatorsIM#line), [link](OperatorsIM#link), [norm](OperatorsNR#norm), [point](OperatorsNR#point), [polygon](OperatorsNR#polygon), [polyline](OperatorsNR#polyline), [rectangle](OperatorsNR#rectangle), [square](OperatorsSZ#square), [triangle](OperatorsSZ#triangle), 