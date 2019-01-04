# Operators (N to R)
 	


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

[//]: # (keyword|operator_nb_cycles)
### `nb_cycles`

#### Possible use: 
  *  **`nb_cycles`** (`graph`) --->  `int` 

#### Result: 
returns the maximum number of independent cycles in a graph. This number (u) is estimated through the number of nodes (v), links (e) and of sub-graphs (p): u = e - v + p.

#### Examples: 
```
graph graphEpidemio <- graph([]);  
int var1 <- nb_cycles(graphEpidemio); // var1 equals the number of cycles in the graph

```
      


#### See also: 

[alpha_index](OperatorsAA#alpha_index), [beta_index](OperatorsBC#beta_index), [gamma_index](OperatorsDH#gamma_index), [connectivity_index](OperatorsBC#connectivity_index), 
    	
----

[//]: # (keyword|operator_neighbors_at)
### `neighbors_at`

#### Possible use: 
  * `geometry` **`neighbors_at`** `float` --->  `list`
  *  **`neighbors_at`** (`geometry` , `float`) --->  `list` 

#### Result: 
a list, containing all the agents of the same species than the left argument (if it is an agent) located at a distance inferior or equal to the right-hand operand to the left-hand operand (geometry, agent, point).  

#### Comment: 
The topology used to compute the neighborhood  is the one of the left-operand if this one is an agent; otherwise the one of the agent applying the operator.

#### Examples: 
```
 
list var0 <- (self neighbors_at (10)); // var0 equals all the agents located at a distance lower or equal to 10 to the agent applying the operator.

```
      


#### See also: 

[neighbors_of](OperatorsNR#neighbors_of), [closest_to](OperatorsBC#closest_to), [overlapping](OperatorsNR#overlapping), [agents_overlapping](OperatorsAA#agents_overlapping), [agents_inside](OperatorsAA#agents_inside), [agent_closest_to](OperatorsAA#agent_closest_to), [at_distance](OperatorsAA#at_distance), 
    	
----

[//]: # (keyword|operator_neighbors_of)
### `neighbors_of`

#### Possible use: 
  * `graph` **`neighbors_of`** `unknown` --->  `list`
  *  **`neighbors_of`** (`graph` , `unknown`) --->  `list`
  * `topology` **`neighbors_of`** `agent` --->  `list`
  *  **`neighbors_of`** (`topology` , `agent`) --->  `list`
  *  **`neighbors_of`** (`topology`, `geometry`, `float`) --->  `list` 

#### Result: 
a list, containing all the agents of the same species than the argument (if it is an agent) located at a distance inferior or equal to 1 to the right-hand operand agent considering the left-hand operand topology.

#### Special cases:     
  * a list, containing all the agents of the same species than the left argument (if it is an agent) located at a distance inferior or equal to the third argument to the second argument (agent, geometry or point) considering the first operand topology. 
  
```
 
list var3 <- neighbors_of (topology(self), self,10); // var3 equals all the agents located at a distance lower or equal to 10 to the agent applying the operator considering its topology.
``` 



#### Examples: 
```
 
list var0 <- graphEpidemio neighbors_of (node(3)); // var0 equals [node0,node2] 
list var1 <- graphFromMap neighbors_of node({12,45}); // var1 equals [{1.0,5.0},{34.0,56.0}] 
list var2 <- topology(self) neighbors_of self; // var2 equals returns all the agents located at a distance lower or equal to 1 to the agent applying the operator considering its topology.

```
      


#### See also: 

[predecessors_of](OperatorsNR#predecessors_of), [successors_of](OperatorsSZ#successors_of), [neighbors_at](OperatorsNR#neighbors_at), [closest_to](OperatorsBC#closest_to), [overlapping](OperatorsNR#overlapping), [agents_overlapping](OperatorsAA#agents_overlapping), [agents_inside](OperatorsAA#agents_inside), [agent_closest_to](OperatorsAA#agent_closest_to), 
    	
----

[//]: # (keyword|operator_new_emotion)
### `new_emotion`

#### Possible use: 
  *  **`new_emotion`** (`string`) --->  `emotion`
  * `string` **`new_emotion`** `agent` --->  `emotion`
  *  **`new_emotion`** (`string` , `agent`) --->  `emotion`
  * `string` **`new_emotion`** `predicate` --->  `emotion`
  *  **`new_emotion`** (`string` , `predicate`) --->  `emotion`
  * `string` **`new_emotion`** `float` --->  `emotion`
  *  **`new_emotion`** (`string` , `float`) --->  `emotion`
  *  **`new_emotion`** (`string`, `predicate`, `agent`) --->  `emotion`
  *  **`new_emotion`** (`string`, `float`, `float`) --->  `emotion`
  *  **`new_emotion`** (`string`, `float`, `agent`) --->  `emotion`
  *  **`new_emotion`** (`string`, `float`, `predicate`) --->  `emotion`
  *  **`new_emotion`** (`string`, `float`, `predicate`, `agent`) --->  `emotion`
  *  **`new_emotion`** (`string`, `float`, `float`, `agent`) --->  `emotion`
  *  **`new_emotion`** (`string`, `float`, `predicate`, `float`) --->  `emotion`
  *  **`new_emotion`** (`string`, `float`, `predicate`, `float`, `agent`) --->  `emotion` 

#### Result: 
a new emotion with the given properties (name)
a new emotion with the given properties (name)
a new emotion with the given properties (name)
a new emotion with the given properties (name,about)
a new emotion with the given properties (name)
a new emotion with the given properties (name,intensity,decay)
a new emotion with the given properties (name)
a new emotion with the given properties (name)
a new emotion with the given properties (name)
a new emotion with the given properties (name, intensity)
a new emotion with the given properties (name)
a new emotion with the given properties (name,intensity,about)

#### Examples: 
```
emotion("joy",12.3,eatFood,4) emotion("joy",12.3,eatFood,4) emotion("joy",12.3,eatFood,4) emotion("joy",eatFood) emotion("joy",12.3,eatFood,4) emotion("joy",12.3,4) emotion("joy",12.3,eatFood,4) emotion("joy",12.3,eatFood,4) emotion("joy",12.3,eatFood,4) emotion("joy",12.3) emotion("joy") emotion("joy",12.3,eatFood) 

```
  
    	
----

[//]: # (keyword|operator_new_folder)
### `new_folder`

#### Possible use: 
  *  **`new_folder`** (`string`) --->  `file` 

#### Result: 
opens an existing repository or create a new folder if it does not exist.

#### Special cases:     
  * If the specified string does not refer to an existing repository, the repository is created.    
  * If the string refers to an existing file, an exception is risen.

#### Examples: 
```
file dirNewT <- new_folder("incl/");   	// dirNewT represents the repository "../incl/" 															// eventually creates the directory ../incl 

```
      


#### See also: 

[folder](OperatorsDH#folder), [file](OperatorsDH#file), 
    	
----

[//]: # (keyword|operator_new_mental_state)
### `new_mental_state`

#### Possible use: 
  *  **`new_mental_state`** (`string`) --->  `mental_state`
  * `string` **`new_mental_state`** `predicate` --->  `mental_state`
  *  **`new_mental_state`** (`string` , `predicate`) --->  `mental_state`
  * `string` **`new_mental_state`** `mental_state` --->  `mental_state`
  *  **`new_mental_state`** (`string` , `mental_state`) --->  `mental_state`
  * `string` **`new_mental_state`** `emotion` --->  `mental_state`
  *  **`new_mental_state`** (`string` , `emotion`) --->  `mental_state`
  *  **`new_mental_state`** (`string`, `emotion`, `int`) --->  `mental_state`
  *  **`new_mental_state`** (`string`, `predicate`, `agent`) --->  `mental_state`
  *  **`new_mental_state`** (`string`, `predicate`, `int`) --->  `mental_state`
  *  **`new_mental_state`** (`string`, `emotion`, `float`) --->  `mental_state`
  *  **`new_mental_state`** (`string`, `predicate`, `float`) --->  `mental_state`
  *  **`new_mental_state`** (`string`, `mental_state`, `float`) --->  `mental_state`
  *  **`new_mental_state`** (`string`, `mental_state`, `int`) --->  `mental_state`
  *  **`new_mental_state`** (`string`, `emotion`, `agent`) --->  `mental_state`
  *  **`new_mental_state`** (`string`, `mental_state`, `agent`) --->  `mental_state`
  *  **`new_mental_state`** (`string`, `mental_state`, `float`, `agent`) --->  `mental_state`
  *  **`new_mental_state`** (`string`, `emotion`, `float`, `agent`) --->  `mental_state`
  *  **`new_mental_state`** (`string`, `predicate`, `float`, `agent`) --->  `mental_state`
  *  **`new_mental_state`** (`string`, `predicate`, `int`, `agent`) --->  `mental_state`
  *  **`new_mental_state`** (`string`, `mental_state`, `float`, `int`) --->  `mental_state`
  *  **`new_mental_state`** (`string`, `emotion`, `float`, `int`) --->  `mental_state`
  *  **`new_mental_state`** (`string`, `predicate`, `float`, `int`) --->  `mental_state`
  *  **`new_mental_state`** (`string`, `emotion`, `int`, `agent`) --->  `mental_state`
  *  **`new_mental_state`** (`string`, `mental_state`, `int`, `agent`) --->  `mental_state`
  *  **`new_mental_state`** (`string`, `mental_state`, `float`, `int`, `agent`) --->  `mental_state`
  *  **`new_mental_state`** (`string`, `predicate`, `float`, `int`, `agent`) --->  `mental_state`
  *  **`new_mental_state`** (`string`, `emotion`, `float`, `int`, `agent`) --->  `mental_state` 

#### Result: 
a new mental state
a new mental state
a new mental state
a new mental state
a new mental state
a new mental state
a new mental state
a new mental state
a new mental state
a new mental state
a new mental state
a new mental state
a new mental state
a new mental state
a new mental state
a new mental state
a new mental state
a new mental state
a new mental state
a new mental state
a new mental state
a new mental state
a new mental state
a new mental state
a new mental state

#### Examples: 
```
new_mental-state(belief) new_mental-state(belief) new_mental-state(belief) new_mental-state(belief) new_mental-state(belief) new_mental-state(belief) new_mental-state(belief) new_mental-state(belief) new_mental-state(belief) new_mental-state(belief) new_mental-state(belief) new_mental-state(belief) new_mental-state(belief) new_mental-state(belief) new_mental-state(belief) new_mental-state(belief) new_mental-state(belief) new_mental-state(belief) new_mental-state(belief) new_mental-state(belief) new_mental-state(belief) new_mental-state(belief) new_mental-state(belief) new_mental-state(belief) new_mental-state(belief) 

```
  
    	
----

[//]: # (keyword|operator_new_predicate)
### `new_predicate`

#### Possible use: 
  *  **`new_predicate`** (`string`) --->  `predicate`
  * `string` **`new_predicate`** `int` --->  `predicate`
  *  **`new_predicate`** (`string` , `int`) --->  `predicate`
  * `string` **`new_predicate`** `agent` --->  `predicate`
  *  **`new_predicate`** (`string` , `agent`) --->  `predicate`
  * `string` **`new_predicate`** `map` --->  `predicate`
  *  **`new_predicate`** (`string` , `map`) --->  `predicate`
  * `string` **`new_predicate`** `bool` --->  `predicate`
  *  **`new_predicate`** (`string` , `bool`) --->  `predicate`
  *  **`new_predicate`** (`string`, `map`, `int`) --->  `predicate`
  *  **`new_predicate`** (`string`, `map`, `bool`) --->  `predicate`
  *  **`new_predicate`** (`string`, `map`, `agent`) --->  `predicate`
  *  **`new_predicate`** (`string`, `map`, `bool`, `agent`) --->  `predicate`
  *  **`new_predicate`** (`string`, `map`, `int`, `bool`) --->  `predicate`
  *  **`new_predicate`** (`string`, `map`, `int`, `agent`) --->  `predicate`
  *  **`new_predicate`** (`string`, `map`, `int`, `bool`, `agent`) --->  `predicate` 

#### Result: 
a new predicate with the given properties (name, values, is_true, agentCause)
a new predicate with the given properties (name, values, lifetime)
a new predicate with the given properties (name)
a new predicate with the given properties (name, values, lifetime, is_true)
a new predicate with the given is_true (name, lifetime)
a new predicate with the given properties (name, values, lifetime, is_true, agentCause)
a new predicate with the given properties (name, values, is_true)
a new predicate with the given properties (name, values, 	agentCause)
a new predicate with the given properties (name, values, lifetime)
a new predicate with the given properties (name, values)
a new predicate with the given properties (name, values, lifetime, agentCause)
a new predicate with the given is_true (name, is_true)

#### Examples: 
```
predicate("people to meet", ["time"::10], true, agentA) predicate("people to meet", ["time"::10], true) predicate("people to meet") predicate("people to meet", ["time"::10], 10,true) predicate("hasWater", 10  predicate("people to meet", ["time"::10], 10, true, agentA) predicate("people to meet", ["time"::10], true) predicate("people to meet", ["time"::10], agentA) predicate("people to meet", ["time"::10], true) predicate("people to meet", people1 ) predicate("people to meet", ["time"::10], 10, agentA) predicate("hasWater", true) 

```
  
    	
----

[//]: # (keyword|operator_new_social_link)
### `new_social_link`

#### Possible use: 
  *  **`new_social_link`** (`agent`) --->  `msi.gaml.architecture.simplebdi.SocialLink`
  *  **`new_social_link`** (`agent`, `float`, `float`, `float`, `float`) --->  `msi.gaml.architecture.simplebdi.SocialLink` 

#### Result: 
a new social link
a new social link

#### Examples: 
```
new_social_link(agentA) new_social_link(agentA,0.0,-0.1,0.2,0.1) 

```
  
    	
----

[//]: # (keyword|operator_node)
### `node`

#### Possible use: 
  *  **`node`** (`unknown`) --->  `unknown`
  * `unknown` **`node`** `float` --->  `unknown`
  *  **`node`** (`unknown` , `float`) --->  `unknown`
    	
----

[//]: # (keyword|operator_nodes)
### `nodes`

#### Possible use: 
  *  **`nodes`** (`container`) --->  `container`
    	
----

[//]: # (keyword|operator_norm)
### `norm`

#### Possible use: 
  *  **`norm`** (`point`) --->  `float` 

#### Result: 
the norm of the vector with the coordinates of the point operand.

#### Examples: 
```
 
float var0 <- norm({3,4}); // var0 equals 5.0

```
  
    	
----

[//]: # (keyword|operator_Norm)
### `Norm`

#### Possible use: 
  *  **`Norm`** (`any`) --->  `Norm` 

#### Result: 
Casts the operand into the type Norm
    	
----

[//]: # (keyword|operator_normal_area)
### `normal_area`

#### Possible use: 
  *  **`normal_area`** (`float`, `float`, `float`) --->  `float` 

#### Result: 
Returns the area to the left of x in the normal distribution with the given mean and standard deviation.
    	
----

[//]: # (keyword|operator_normal_density)
### `normal_density`

#### Possible use: 
  *  **`normal_density`** (`float`, `float`, `float`) --->  `float` 

#### Result: 
Returns the probability of x in the normal distribution with the given mean and standard deviation.
    	
----

[//]: # (keyword|operator_normal_inverse)
### `normal_inverse`

#### Possible use: 
  *  **`normal_inverse`** (`float`, `float`, `float`) --->  `float` 

#### Result: 
Returns the x in the normal distribution with the given mean and standard deviation, to the left of which lies the given area. normal.Inverse returns the value in terms of standard deviations from the mean, so we need to adjust it for the given mean and standard deviation.
    	
----

[//]: # (keyword|operator_not)
### `not`
   Same signification as [!](OperatorsAA#!)
    	
----

[//]: # (keyword|operator_obj_file)
### `obj_file`

#### Possible use: 
  *  **`obj_file`** (`string`) --->  `file` 

#### Result: 
Constructs a file of type obj. Allowed extensions are limited to obj, OBJ
    	
----

[//]: # (keyword|operator_of)
### `of`
   Same signification as [.](OperatorsAA#.)
    	
----

[//]: # (keyword|operator_of_generic_species)
### `of_generic_species`

#### Possible use: 
  * `container` **`of_generic_species`** `species` --->  `list`
  *  **`of_generic_species`** (`container` , `species`) --->  `list` 

#### Result: 
a list, containing the agents of the left-hand operand whose species is that denoted by the right-hand operand and whose species extends the right-hand operand species

#### Examples: 
```
// species test {} // species sous_test parent: test {}  
list var2 <- [sous_test(0),sous_test(1),test(2),test(3)] of_generic_species test; // var2 equals [sous_test0,sous_test1,test2,test3] 
list var3 <- [sous_test(0),sous_test(1),test(2),test(3)] of_generic_species sous_test; // var3 equals [sous_test0,sous_test1] 
list var4 <- [sous_test(0),sous_test(1),test(2),test(3)] of_species test; // var4 equals [test2,test3] 
list var5 <- [sous_test(0),sous_test(1),test(2),test(3)] of_species sous_test; // var5 equals [sous_test0,sous_test1]

```
      


#### See also: 

[of_species](OperatorsNR#of_species), 
    	
----

[//]: # (keyword|operator_of_species)
### `of_species`

#### Possible use: 
  * `container` **`of_species`** `species` --->  `list`
  *  **`of_species`** (`container` , `species`) --->  `list` 

#### Result: 
a list, containing the agents of the left-hand operand whose species is the one denoted by the right-hand operand.The expression agents of_species (species self) is equivalent to agents where (species each = species self); however, the advantage of using the first syntax is that the resulting list is correctly typed with the right species, whereas, in the second syntax, the parser cannot determine the species of the agents within the list (resulting in the need to cast it explicitly if it is to be used in an ask statement, for instance).

#### Special cases:     
  * if the right operand is nil, of_species returns the right operand

#### Examples: 
```
 
list var0 <- (self neighbors_at 10) of_species (species (self)); // var0 equals all the neighboring agents of the same species. 
list var1 <- [test(0),test(1),node(1),node(2)] of_species test; // var1 equals [test0,test1]

```
      


#### See also: 

[of_generic_species](OperatorsNR#of_generic_species), 
    	
----

[//]: # (keyword|operator_one_of)
### `one_of`

#### Possible use: 
  *  **`one_of`** (`container<KeyType,ValueType>`) --->  `ValueType` 

#### Result: 
one of the values stored in this container  at a random key  

#### Comment: 
the one_of operator behavior depends on the nature of the operand

#### Special cases:     
  * if it is a graph, one_of returns one of the lists of edges    
  * if it is a file, one_of returns one of the elements of the content of the file (that is also a container)    
  * if the operand is empty, one_of returns nil 
  
```

``` 

    
  * if it is a list or a matrix, one_of returns one of the values of the list or of the matrix 
  
```
int 
i <- any ([1,2,3]); //i equals 1, 2 or 3string sMat <- one_of(matrix([["c11","c12","c13"],["c21","c22","c23"]])); 	// sMat equals "c11","c12","c13", "c21","c22" or "c23" 
``` 

    
  * if it is a map, one_of returns one the value of a random pair of the map 
  
```
int im <- one_of ([2::3, 4::5, 6::7]);	// im equals 3, 5 or 7  
bool var6 <- [2::3, 4::5, 6::7].values contains im; // var6 equals true
``` 

    
  * if it is a population, one_of returns one of the agents of the population 
  
```
bug b <- one_of(bug);  	// Given a previously defined species bug, b is one of the created bugs, e.g. bug3 
``` 

    


#### See also: 

[contains](OperatorsBC#contains), 
    	
----

[//]: # (keyword|operator_open_simplex_generator)
### `open_simplex_generator`

#### Possible use: 
  *  **`open_simplex_generator`** (`float`, `float`, `float`) --->  `float` 

#### Result: 
take a x, y and a bias parameters and gives a value

#### Examples: 
```
 
float var0 <- open_simplex_generator(2,3,253); // var0 equals 10.2

```
  
    	
----

[//]: # (keyword|operator_or)
### `or`

#### Possible use: 
  * `bool` **`or`** `any expression` --->  `bool`
  *  **`or`** (`bool` , `any expression`) --->  `bool` 

#### Result: 
a bool value, equal to the logical or between the left-hand operand and the right-hand operand.  

#### Comment: 
both operands are always casted to bool before applying the operator. Thus, an expression like 1 or 0 is accepted and returns true.    


#### See also: 

[bool](OperatorsBC#bool), [and](OperatorsAA#and), [!](OperatorsAA#!), 
    	
----

[//]: # (keyword|operator_or)
### `or`

#### Possible use: 
  * `predicate` **`or`** `predicate` --->  `predicate`
  *  **`or`** (`predicate` , `predicate`) --->  `predicate` 

#### Result: 
create a new predicate from two others by including them as subintentions. It's an exclusive "or"

#### Examples: 
```
predicate1 or predicate2 

```
  
    	
----

[//]: # (keyword|operator_osm_file)
### `osm_file`

#### Possible use: 
  * `string` **`osm_file`** `map<string,list>` --->  `file`
  *  **`osm_file`** (`string` , `map<string,list>`) --->  `file`
  *  **`osm_file`** (`string`, `map<string,list>`, `int`) --->  `file` 

#### Result: 
opens a file that a is a kind of OSM file with some filtering, forcing the initial CRS to be the one indicated by the second int parameter (see http://spatialreference.org/ref/epsg/). If this int parameter is equal to 0, the data is considered as already projected.
opens a file that a is a kind of OSM file with some filtering.  

#### Comment: 
The file should have a OSM file extension, cf. file type definition for supported file extensions.The file should have a OSM file extension, cf. file type definition for supported file extensions.

#### Special cases:     
  * If the specified string does not refer to an existing OSM file, an exception is risen.    
  * If the specified string does not refer to an existing OSM file, an exception is risen.

#### Examples: 
```
file myOSMfile2 <- osm_file("../includes/rouen.osm",["highway"::["primary","motorway"]], 0); file myOSMfile <- osm_file("../includes/rouen.osm", ["highway"::["primary","motorway"]]); 

```
      


#### See also: 

[file](OperatorsDH#file), 
    	
----

[//]: # (keyword|operator_out_degree_of)
### `out_degree_of`

#### Possible use: 
  * `graph` **`out_degree_of`** `unknown` --->  `int`
  *  **`out_degree_of`** (`graph` , `unknown`) --->  `int` 

#### Result: 
returns the out degree of a vertex (right-hand operand) in the graph given as left-hand operand.

#### Examples: 
```
 
int var1 <- graphFromMap out_degree_of (node(3)); // var1 equals 4

```
      


#### See also: 

[in_degree_of](OperatorsIM#in_degree_of), [degree_of](OperatorsDH#degree_of), 
    	
----

[//]: # (keyword|operator_out_edges_of)
### `out_edges_of`

#### Possible use: 
  * `graph` **`out_edges_of`** `unknown` --->  `list`
  *  **`out_edges_of`** (`graph` , `unknown`) --->  `list` 

#### Result: 
returns the list of the out-edges of a vertex (right-hand operand) in the graph given as left-hand operand.

#### Examples: 
```
 
list var1 <- graphFromMap out_edges_of (node(3)); // var1 equals 3

```
      


#### See also: 

[in_edges_of](OperatorsIM#in_edges_of), 
    	
----

[//]: # (keyword|operator_overlapping)
### `overlapping`

#### Possible use: 
  * `container<agent>` **`overlapping`** `geometry` --->  `list<geometry>`
  *  **`overlapping`** (`container<agent>` , `geometry`) --->  `list<geometry>` 

#### Result: 
A list of agents or geometries among the left-operand list, species or meta-population (addition of species), overlapping the operand (casted as a geometry).

#### Examples: 
```
 
list<geometry> var0 <- [ag1, ag2, ag3] overlapping(self); // var0 equals return the agents among ag1, ag2 and ag3 that overlap the shape of the agent applying the operator.(species1 + species2) overlapping self 

```
      


#### See also: 

[neighbors_at](OperatorsNR#neighbors_at), [neighbors_of](OperatorsNR#neighbors_of), [agent_closest_to](OperatorsAA#agent_closest_to), [agents_inside](OperatorsAA#agents_inside), [closest_to](OperatorsBC#closest_to), [inside](OperatorsIM#inside), [agents_overlapping](OperatorsAA#agents_overlapping), 
    	
----

[//]: # (keyword|operator_overlaps)
### `overlaps`

#### Possible use: 
  * `geometry` **`overlaps`** `geometry` --->  `bool`
  *  **`overlaps`** (`geometry` , `geometry`) --->  `bool` 

#### Result: 
A boolean, equal to true if the left-geometry (or agent/point) overlaps the right-geometry (or agent/point).

#### Special cases:     
  * if one of the operand is null, returns false.    
  * if one operand is a point, returns true if the point is included in the geometry

#### Examples: 
```
 
bool var0 <- polyline([{10,10},{20,20}]) overlaps polyline([{15,15},{25,25}]); // var0 equals true 
bool var1 <- polygon([{10,10},{10,20},{20,20},{20,10}]) overlaps polygon([{15,15},{15,25},{25,25},{25,15}]); // var1 equals true 
bool var2 <- polygon([{10,10},{10,20},{20,20},{20,10}]) overlaps {25,25}; // var2 equals false 
bool var3 <- polygon([{10,10},{10,20},{20,20},{20,10}]) overlaps polygon([{35,35},{35,45},{45,45},{45,35}]); // var3 equals false 
bool var4 <- polygon([{10,10},{10,20},{20,20},{20,10}]) overlaps polyline([{10,10},{20,20}]); // var4 equals true 
bool var5 <- polygon([{10,10},{10,20},{20,20},{20,10}]) overlaps {15,15}; // var5 equals true 
bool var6 <- polygon([{10,10},{10,20},{20,20},{20,10}]) overlaps polygon([{0,0},{0,30},{30,30}, {30,0}]); // var6 equals true 
bool var7 <- polygon([{10,10},{10,20},{20,20},{20,10}]) overlaps polygon([{15,15},{15,25},{25,25},{25,15}]); // var7 equals true 
bool var8 <- polygon([{10,10},{10,20},{20,20},{20,10}]) overlaps polygon([{10,20},{20,20},{20,30},{10,30}]); // var8 equals true

```
      


#### See also: 

[disjoint_from](OperatorsDH#disjoint_from), [crosses](OperatorsBC#crosses), [intersects](OperatorsIM#intersects), [partially_overlaps](OperatorsNR#partially_overlaps), [touches](OperatorsSZ#touches), 
    	
----

[//]: # (keyword|operator_pair)
### `pair`

#### Possible use: 
  *  **`pair`** (`any`) --->  `pair` 

#### Result: 
Casts the operand into the type pair
    	
----

[//]: # (keyword|operator_partially_overlaps)
### `partially_overlaps`

#### Possible use: 
  * `geometry` **`partially_overlaps`** `geometry` --->  `bool`
  *  **`partially_overlaps`** (`geometry` , `geometry`) --->  `bool` 

#### Result: 
A boolean, equal to true if the left-geometry (or agent/point) partially overlaps the right-geometry (or agent/point).  

#### Comment: 
if one geometry operand fully covers the other geometry operand, returns false (contrarily to the overlaps operator).

#### Special cases:     
  * if one of the operand is null, returns false.

#### Examples: 
```
 
bool var0 <- polyline([{10,10},{20,20}]) partially_overlaps polyline([{15,15},{25,25}]); // var0 equals true 
bool var1 <- polygon([{10,10},{10,20},{20,20},{20,10}]) partially_overlaps polygon([{15,15},{15,25},{25,25},{25,15}]); // var1 equals true 
bool var2 <- polygon([{10,10},{10,20},{20,20},{20,10}]) partially_overlaps {25,25}; // var2 equals false 
bool var3 <- polygon([{10,10},{10,20},{20,20},{20,10}]) partially_overlaps polygon([{35,35},{35,45},{45,45},{45,35}]); // var3 equals false 
bool var4 <- polygon([{10,10},{10,20},{20,20},{20,10}]) partially_overlaps polyline([{10,10},{20,20}]); // var4 equals false 
bool var5 <- polygon([{10,10},{10,20},{20,20},{20,10}]) partially_overlaps {15,15}; // var5 equals false 
bool var6 <- polygon([{10,10},{10,20},{20,20},{20,10}]) partially_overlaps polygon([{0,0},{0,30},{30,30}, {30,0}]); // var6 equals false 
bool var7 <- polygon([{10,10},{10,20},{20,20},{20,10}]) partially_overlaps polygon([{15,15},{15,25},{25,25},{25,15}]); // var7 equals true 
bool var8 <- polygon([{10,10},{10,20},{20,20},{20,10}]) partially_overlaps polygon([{10,20},{20,20},{20,30},{10,30}]); // var8 equals false

```
      


#### See also: 

[disjoint_from](OperatorsDH#disjoint_from), [crosses](OperatorsBC#crosses), [overlaps](OperatorsNR#overlaps), [intersects](OperatorsIM#intersects), [touches](OperatorsSZ#touches), 
    	
----

[//]: # (keyword|operator_path)
### `path`

#### Possible use: 
  *  **`path`** (`any`) --->  `path` 

#### Result: 
Casts the operand into the type path
    	
----

[//]: # (keyword|operator_path_between)
### `path_between`

#### Possible use: 
  * `topology` **`path_between`** `container<geometry>` --->  `path`
  *  **`path_between`** (`topology` , `container<geometry>`) --->  `path`
  * `msi.gama.util.GamaMap<msi.gama.metamodel.agent.IAgent,java.lang.Object>` **`path_between`** `container<geometry>` --->  `path`
  *  **`path_between`** (`msi.gama.util.GamaMap<msi.gama.metamodel.agent.IAgent,java.lang.Object>` , `container<geometry>`) --->  `path`
  * `list<agent>` **`path_between`** `container<geometry>` --->  `path`
  *  **`path_between`** (`list<agent>` , `container<geometry>`) --->  `path`
  *  **`path_between`** (`topology`, `geometry`, `geometry`) --->  `path`
  *  **`path_between`** (`list<agent>`, `geometry`, `geometry`) --->  `path`
  *  **`path_between`** (`graph`, `geometry`, `geometry`) --->  `path`
  *  **`path_between`** (`msi.gama.util.GamaMap<msi.gama.metamodel.agent.IAgent,java.lang.Object>`, `geometry`, `geometry`) --->  `path` 

#### Result: 
The shortest path between two objects according to set of cells
The shortest path between a list of two objects in a graph
The shortest path between two objects according to set of cells with corresponding weights
The shortest path between several objects according to set of cells with corresponding weights
The shortest path between several objects according to set of cells

#### Examples: 
```
 
path var0 <- my_topology path_between (ag1, ag2); // var0 equals A path between ag1 and ag2 
path var1 <- path_between (cell_grid where each.is_free, ag1, ag2); // var1 equals A path between ag1 and ag2 passing through the given cell_grid agents 
path var2 <- my_topology path_between [ag1, ag2]; // var2 equals A path between ag1 and ag2 
path var3 <- path_between (my_graph, ag1, ag2); // var3 equals A path between ag1 and ag2 
path var4 <- path_between (cell_grid as_map (each::each.is_obstacle ? 9999.0 : 1.0), ag1, ag2); // var4 equals A path between ag1 and ag2 passing through the given cell_grid agents with a minimal cost 
path var5 <- path_between (cell_grid as_map (each::each.is_obstacle ? 9999.0 : 1.0), [ag1, ag2, ag3]); // var5 equals A path between ag1 and ag2 and ag3 passing through the given cell_grid agents with minimal cost 
path var6 <- path_between (cell_grid where each.is_free, [ag1, ag2, ag3]); // var6 equals A path between ag1 and ag2 and ag3 passing through the given cell_grid agents

```
      


#### See also: 

[towards](OperatorsSZ#towards), [direction_to](OperatorsDH#direction_to), [distance_between](OperatorsDH#distance_between), [direction_between](OperatorsDH#direction_between), [path_to](OperatorsNR#path_to), [distance_to](OperatorsDH#distance_to), 
    	
----

[//]: # (keyword|operator_path_to)
### `path_to`

#### Possible use: 
  * `point` **`path_to`** `point` --->  `path`
  *  **`path_to`** (`point` , `point`) --->  `path`
  * `geometry` **`path_to`** `geometry` --->  `path`
  *  **`path_to`** (`geometry` , `geometry`) --->  `path` 

#### Result: 
A path between two geometries (geometries, agents or points) considering the topology of the agent applying the operator.

#### Examples: 
```
 
path var0 <- ag1 path_to ag2; // var0 equals the path between ag1 and ag2 considering the topology of the agent applying the operator

```
      


#### See also: 

[towards](OperatorsSZ#towards), [direction_to](OperatorsDH#direction_to), [distance_between](OperatorsDH#distance_between), [direction_between](OperatorsDH#direction_between), [path_between](OperatorsNR#path_between), [distance_to](OperatorsDH#distance_to), 
    	
----

[//]: # (keyword|operator_paths_between)
### `paths_between`

#### Possible use: 
  *  **`paths_between`** (`graph`, `pair`, `int`) --->  `msi.gama.util.IList<msi.gama.util.path.GamaSpatialPath>` 

#### Result: 
The K shortest paths between a list of two objects in a graph

#### Examples: 
```
 
msi.gama.util.IList<msi.gama.util.path.GamaSpatialPath> var0 <- paths_between(my_graph, ag1:: ag2, 2); // var0 equals the 2 shortest paths (ordered by length) between ag1 and ag2

```
  
    	
----

[//]: # (keyword|operator_pbinom)
### `pbinom`
   Same signification as [binomial_sum](OperatorsBC#binomial_sum)
    	
----

[//]: # (keyword|operator_pchisq)
### `pchisq`
   Same signification as [chi_square](OperatorsBC#chi_square)
    	
----

[//]: # (keyword|operator_percent_absolute_deviation)
### `percent_absolute_deviation`

#### Possible use: 
  * `list<float>` **`percent_absolute_deviation`** `list<float>` --->  `float`
  *  **`percent_absolute_deviation`** (`list<float>` , `list<float>`) --->  `float` 

#### Result: 
percent absolute deviation indicator for 2 series of values: percent_absolute_deviation(list_vals_observe,list_vals_sim)

#### Examples: 
```
percent_absolute_deviation([200,300,150,150,200],[250,250,100,200,200]) 

```
  
    	
----

[//]: # (keyword|operator_percentile)
### `percentile`
   Same signification as [quantile_inverse](OperatorsNR#quantile_inverse)
    	
----

[//]: # (keyword|operator_pgamma)
### `pgamma`
   Same signification as [gamma_distribution](OperatorsDH#gamma_distribution)
    	
----

[//]: # (keyword|operator_pgm_file)
### `pgm_file`

#### Possible use: 
  *  **`pgm_file`** (`string`) --->  `file` 

#### Result: 
Constructs a file of type pgm. Allowed extensions are limited to pgm
    	
----

[//]: # (keyword|operator_plan)
### `plan`

#### Possible use: 
  * `container<geometry>` **`plan`** `float` --->  `geometry`
  *  **`plan`** (`container<geometry>` , `float`) --->  `geometry` 

#### Result: 
A polyline geometry from the given list of points.

#### Special cases:     
  * if the operand is nil, returns the point geometry {0,0}    
  * if the operand is composed of a single point, returns a point geometry.

#### Examples: 
```
 
geometry var0 <- polyplan([{0,0}, {0,10}, {10,10}, {10,0}],10); // var0 equals a polyline geometry composed of the 4 points with a depth of 10.

```
      


#### See also: 

[around](OperatorsAA#around), [circle](OperatorsBC#circle), [cone](OperatorsBC#cone), [link](OperatorsIM#link), [norm](OperatorsNR#norm), [point](OperatorsNR#point), [polygone](OperatorsSZ#polygone), [rectangle](OperatorsNR#rectangle), [square](OperatorsSZ#square), [triangle](OperatorsSZ#triangle), 
    	
----

[//]: # (keyword|operator_plus_days)
### `plus_days`

#### Possible use: 
  * `date` **`plus_days`** `int` --->  `date`
  *  **`plus_days`** (`date` , `int`) --->  `date` 

#### Result: 
Add a given number of days to a date

#### Examples: 
```
 
date var0 <- date('2000-01-01') plus_days 12; // var0 equals date('2000-01-13')

```
  
    	
----

[//]: # (keyword|operator_plus_hours)
### `plus_hours`

#### Possible use: 
  * `date` **`plus_hours`** `int` --->  `date`
  *  **`plus_hours`** (`date` , `int`) --->  `date` 

#### Result: 
Add a given number of hours to a date

#### Examples: 
```
// equivalent to date1 + 15 #h  
date var1 <- date('2000-01-01') plus_hours 24; // var1 equals date('2000-01-02')

```
  
    	
----

[//]: # (keyword|operator_plus_minutes)
### `plus_minutes`

#### Possible use: 
  * `date` **`plus_minutes`** `int` --->  `date`
  *  **`plus_minutes`** (`date` , `int`) --->  `date` 

#### Result: 
Add a given number of minutes to a date

#### Examples: 
```
// equivalent to date1 + 5 #mn  
date var1 <- date('2000-01-01') plus_minutes 5 ; // var1 equals date('2000-01-01 00:05:00')

```
  
    	
----

[//]: # (keyword|operator_plus_months)
### `plus_months`

#### Possible use: 
  * `date` **`plus_months`** `int` --->  `date`
  *  **`plus_months`** (`date` , `int`) --->  `date` 

#### Result: 
Add a given number of months to a date

#### Examples: 
```
 
date var0 <- date('2000-01-01') plus_months 5; // var0 equals date('2000-06-01')

```
  
    	
----

[//]: # (keyword|operator_plus_ms)
### `plus_ms`

#### Possible use: 
  * `date` **`plus_ms`** `int` --->  `date`
  *  **`plus_ms`** (`date` , `int`) --->  `date` 

#### Result: 
Add a given number of milliseconds to a date

#### Examples: 
```
// equivalent to date('2000-01-01') + 15 #ms  
date var1 <- date('2000-01-01') plus_ms 1000 ; // var1 equals date('2000-01-01 00:00:01')

```
  
    	
----

[//]: # (keyword|operator_plus_seconds)
### `plus_seconds`
   Same signification as [+](OperatorsAA#+)
    	
----

[//]: # (keyword|operator_plus_weeks)
### `plus_weeks`

#### Possible use: 
  * `date` **`plus_weeks`** `int` --->  `date`
  *  **`plus_weeks`** (`date` , `int`) --->  `date` 

#### Result: 
Add a given number of weeks to a date

#### Examples: 
```
 
date var0 <- date('2000-01-01') plus_weeks 15; // var0 equals date('2000-04-15')

```
  
    	
----

[//]: # (keyword|operator_plus_years)
### `plus_years`

#### Possible use: 
  * `date` **`plus_years`** `int` --->  `date`
  *  **`plus_years`** (`date` , `int`) --->  `date` 

#### Result: 
Add a given number of years to a date

#### Examples: 
```
 
date var0 <- date('2000-01-01') plus_years 15; // var0 equals date('2015-01-01')

```
  
    	
----

[//]: # (keyword|operator_pnorm)
### `pnorm`
   Same signification as [normal_area](OperatorsNR#normal_area)
    	
----

[//]: # (keyword|operator_point)
### `point`

#### Possible use: 
  *  **`point`** (`any`) --->  `point` 

#### Result: 
Casts the operand into the type point
    	
----

[//]: # (keyword|operator_points_along)
### `points_along`

#### Possible use: 
  * `geometry` **`points_along`** `list<float>` --->  `list`
  *  **`points_along`** (`geometry` , `list<float>`) --->  `list` 

#### Result: 
A list of points along the operand-geometry given its location in terms of rate of distance from the starting points of the geometry.

#### Examples: 
```
 
list var0 <-  line([{10,10},{80,80}]) points_along ([0.3, 0.5, 0.9]); // var0 equals the list of following points: [{31.0,31.0,0.0},{45.0,45.0,0.0},{73.0,73.0,0.0}]

```
      


#### See also: 

[closest_points_with](OperatorsBC#closest_points_with), [farthest_point_to](OperatorsDH#farthest_point_to), [points_at](OperatorsNR#points_at), [points_on](OperatorsNR#points_on), 
    	
----

[//]: # (keyword|operator_points_at)
### `points_at`

#### Possible use: 
  * `int` **`points_at`** `float` --->  `list<point>`
  *  **`points_at`** (`int` , `float`) --->  `list<point>` 

#### Result: 
A list of left-operand number of points located at a the right-operand distance to the agent location.

#### Examples: 
```
 
list<point> var0 <- 3 points_at(20.0); // var0 equals returns [pt1, pt2, pt3] with pt1, pt2 and pt3 located at a distance of 20.0 to the agent location

```
      


#### See also: 

[any_location_in](OperatorsAA#any_location_in), [any_point_in](OperatorsAA#any_point_in), [closest_points_with](OperatorsBC#closest_points_with), [farthest_point_to](OperatorsDH#farthest_point_to), 
    	
----

[//]: # (keyword|operator_points_on)
### `points_on`

#### Possible use: 
  * `geometry` **`points_on`** `float` --->  `list`
  *  **`points_on`** (`geometry` , `float`) --->  `list` 

#### Result: 
A list of points of the operand-geometry distant from each other to the float right-operand .

#### Examples: 
```
 
list var0 <-  square(5) points_on(2); // var0 equals a list of points belonging to the exterior ring of the square distant from each other of 2.

```
      


#### See also: 

[closest_points_with](OperatorsBC#closest_points_with), [farthest_point_to](OperatorsDH#farthest_point_to), [points_at](OperatorsNR#points_at), 
    	
----

[//]: # (keyword|operator_poisson)
### `poisson`

#### Possible use: 
  *  **`poisson`** (`float`) --->  `int` 

#### Result: 
A value from a random variable following a Poisson distribution (with the positive expected number of occurence lambda as operand).  

#### Comment: 
The Poisson distribution is a discrete probability distribution that expresses the probability of a given number of events occurring in a fixed interval of time and/or space if these events occur with a known average rate and independently of the time since the last event, cf. Poisson distribution on Wikipedia.

#### Examples: 
```
 
int var0 <- poisson(3.5); // var0 equals a random positive integer

```
      


#### See also: 

[binomial](OperatorsBC#binomial), [gauss](OperatorsDH#gauss), 
    	
----

[//]: # (keyword|operator_polygon)
### `polygon`

#### Possible use: 
  *  **`polygon`** (`container<agent>`) --->  `geometry` 

#### Result: 
A polygon geometry from the given list of points.

#### Special cases:     
  * if the operand is nil, returns the point geometry {0,0}    
  * if the operand is composed of a single point, returns a point geometry    
  * if the operand is composed of 2 points, returns a polyline geometry.

#### Examples: 
```
 
geometry var0 <- polygon([{0,0}, {0,10}, {10,10}, {10,0}]); // var0 equals a polygon geometry composed of the 4 points.

```
      


#### See also: 

[around](OperatorsAA#around), [circle](OperatorsBC#circle), [cone](OperatorsBC#cone), [line](OperatorsIM#line), [link](OperatorsIM#link), [norm](OperatorsNR#norm), [point](OperatorsNR#point), [polyline](OperatorsNR#polyline), [rectangle](OperatorsNR#rectangle), [square](OperatorsSZ#square), [triangle](OperatorsSZ#triangle), 
    	
----

[//]: # (keyword|operator_polyhedron)
### `polyhedron`

#### Possible use: 
  * `container<geometry>` **`polyhedron`** `float` --->  `geometry`
  *  **`polyhedron`** (`container<geometry>` , `float`) --->  `geometry` 

#### Result: 
A polyhedron geometry from the given list of points.

#### Special cases:     
  * if the operand is nil, returns the point geometry {0,0}    
  * if the operand is composed of a single point, returns a point geometry    
  * if the operand is composed of 2 points, returns a polyline geometry.

#### Examples: 
```
 
geometry var0 <- polyhedron([{0,0}, {0,10}, {10,10}, {10,0}],10); // var0 equals a polygon geometry composed of the 4 points and of depth 10.

```
      


#### See also: 

[around](OperatorsAA#around), [circle](OperatorsBC#circle), [cone](OperatorsBC#cone), [line](OperatorsIM#line), [link](OperatorsIM#link), [norm](OperatorsNR#norm), [point](OperatorsNR#point), [polyline](OperatorsNR#polyline), [rectangle](OperatorsNR#rectangle), [square](OperatorsSZ#square), [triangle](OperatorsSZ#triangle), 
    	
----

[//]: # (keyword|operator_polyline)
### `polyline`
   Same signification as [line](OperatorsIM#line)
    	
----

[//]: # (keyword|operator_polyplan)
### `polyplan`
   Same signification as [plan](OperatorsNR#plan)
    	
----

[//]: # (keyword|operator_predecessors_of)
### `predecessors_of`

#### Possible use: 
  * `graph` **`predecessors_of`** `unknown` --->  `list`
  *  **`predecessors_of`** (`graph` , `unknown`) --->  `list` 

#### Result: 
returns the list of predecessors (i.e. sources of in edges) of the given vertex (right-hand operand) in the given graph (left-hand operand)

#### Examples: 
```
 
list var1 <- graphEpidemio predecessors_of ({1,5}); // var1 equals [] 
list var2 <- graphEpidemio predecessors_of node({34,56}); // var2 equals [{12;45}]

```
      


#### See also: 

[neighbors_of](OperatorsNR#neighbors_of), [successors_of](OperatorsSZ#successors_of), 
    	
----

[//]: # (keyword|operator_predicate)
### `predicate`

#### Possible use: 
  *  **`predicate`** (`any`) --->  `predicate` 

#### Result: 
Casts the operand into the type predicate
    	
----

[//]: # (keyword|operator_predict)
### `predict`

#### Possible use: 
  * `regression` **`predict`** `list<float>` --->  `float`
  *  **`predict`** (`regression` , `list<float>`) --->  `float` 

#### Result: 
returns the value predict by the regression parameters for a given instance. Usage: predict(regression, instance)

#### Examples: 
```
predict(my_regression, [1,2,3]) 

```
  
    	
----

[//]: # (keyword|operator_product)
### `product`
   Same signification as [mul](OperatorsIM#mul)
    	
----

[//]: # (keyword|operator_product_of)
### `product_of`

#### Possible use: 
  * `container` **`product_of`** `any expression` --->  `unknown`
  *  **`product_of`** (`container` , `any expression`) --->  `unknown` 

#### Result: 
the product of the right-hand expression evaluated on each of the elements of the left-hand operand  

#### Comment: 
in the right-hand operand, the keyword each can be used to represent, in turn, each of the right-hand operand elements.

#### Special cases:     
  * if the left-operand is a map, the keyword each will contain each value 
  
```
 
unknown var1 <- [1::2, 3::4, 5::6] product_of (each); // var1 equals 48
``` 



#### Examples: 
```
 
unknown var0 <- [1,2] product_of (each * 10 ); // var0 equals 200

```
      


#### See also: 

[min_of](OperatorsIM#min_of), [max_of](OperatorsIM#max_of), [sum_of](OperatorsSZ#sum_of), [mean_of](OperatorsIM#mean_of), 
    	
----

[//]: # (keyword|operator_promethee_DM)
### `promethee_DM`

#### Possible use: 
  * `msi.gama.util.IList<java.util.List>` **`promethee_DM`** `msi.gama.util.IList<java.util.Map<java.lang.String,java.lang.Object>>` --->  `int`
  *  **`promethee_DM`** (`msi.gama.util.IList<java.util.List>` , `msi.gama.util.IList<java.util.Map<java.lang.String,java.lang.Object>>`) --->  `int` 

#### Result: 
The index of the best candidate according to the Promethee II method. This method is based on a comparison per pair of possible candidates along each criterion: all candidates are compared to each other by pair and ranked. More information about this method can be found in [http://www.sciencedirect.com/science?_ob=ArticleURL&_udi=B6VCT-4VF56TV-1&_user=10&_coverDate=01%2F01%2F2010&_rdoc=1&_fmt=high&_orig=search&_sort=d&_docanchor=&view=c&_searchStrId=1389284642&_rerunOrigin=google&_acct=C000050221&_version=1&_urlVersion=0&_userid=10&md5=d334de2a4e0d6281199a39857648cd36 Behzadian, M., Kazemzadeh, R., Albadvi, A., M., A.: PROMETHEE: A comprehensive literature review on methodologies and applications. European Journal of Operational Research(2009)]. The first operand is the list of candidates (a candidate is a list of criterion values); the second operand the list of criterion: A criterion is a map that contains fours elements: a name, a weight, a preference value (p) and an indifference value (q). The preference value represents the threshold from which the difference between two criterion values allows to prefer one vector of values over another. The indifference value represents the threshold from which the difference between two criterion values is considered significant.

#### Special cases:     
  * returns -1 is the list of candidates is nil or empty

#### Examples: 
```
 
int var0 <- promethee_DM([[1.0, 7.0],[4.0,2.0],[3.0, 3.0]], [["name"::"utility", "weight" :: 2.0,"p"::0.5, "q"::0.0, "s"::1.0, "maximize" :: true],["name"::"price", "weight" :: 1.0,"p"::0.5, "q"::0.0, "s"::1.0, "maximize" :: false]]); // var0 equals 1

```
      


#### See also: 

[weighted_means_DM](OperatorsSZ#weighted_means_dm), [electre_DM](OperatorsDH#electre_dm), [evidence_theory_DM](OperatorsDH#evidence_theory_dm), 
    	
----

[//]: # (keyword|operator_property_file)
### `property_file`

#### Possible use: 
  *  **`property_file`** (`string`) --->  `file` 

#### Result: 
Constructs a file of type property. Allowed extensions are limited to properties
    	
----

[//]: # (keyword|operator_pValue_for_fStat)
### `pValue_for_fStat`

#### Possible use: 
  *  **`pValue_for_fStat`** (`float`, `int`, `int`) --->  `float` 

#### Result: 
Returns the P value of F statistic fstat with numerator degrees of freedom dfn and denominator degress of freedom dfd. Uses the incomplete Beta function.
    	
----

[//]: # (keyword|operator_pValue_for_tStat)
### `pValue_for_tStat`

#### Possible use: 
  * `float` **`pValue_for_tStat`** `int` --->  `float`
  *  **`pValue_for_tStat`** (`float` , `int`) --->  `float` 

#### Result: 
Returns the P value of the T statistic tstat with df degrees of freedom. This is a two-tailed test so we just double the right tail which is given by studentT of -|tstat|.
    	
----

[//]: # (keyword|operator_pyramid)
### `pyramid`

#### Possible use: 
  *  **`pyramid`** (`float`) --->  `geometry` 

#### Result: 
A square geometry which side size is given by the operand.  

#### Comment: 
the center of the pyramid is by default the location of the current agent in which has been called this operator.

#### Special cases:     
  * returns nil if the operand is nil.

#### Examples: 
```
 
geometry var0 <- pyramid(5); // var0 equals a geometry as a square with side_size = 5.

```
      


#### See also: 

[around](OperatorsAA#around), [circle](OperatorsBC#circle), [cone](OperatorsBC#cone), [line](OperatorsIM#line), [link](OperatorsIM#link), [norm](OperatorsNR#norm), [point](OperatorsNR#point), [polygon](OperatorsNR#polygon), [polyline](OperatorsNR#polyline), [rectangle](OperatorsNR#rectangle), [square](OperatorsSZ#square), 
    	
----

[//]: # (keyword|operator_quantile)
### `quantile`

#### Possible use: 
  * `container` **`quantile`** `float` --->  `float`
  *  **`quantile`** (`container` , `float`) --->  `float` 

#### Result: 
Returns the phi-quantile; that is, an element elem for which holds that phi percent of data elements are less than elem. The quantile need not necessarily be contained in the data sequence, it can be a linear interpolation. Note that the container holding the values must be sorted first
    	
----

[//]: # (keyword|operator_quantile_inverse)
### `quantile_inverse`

#### Possible use: 
  * `container` **`quantile_inverse`** `float` --->  `float`
  *  **`quantile_inverse`** (`container` , `float`) --->  `float` 

#### Result: 
Returns how many percent of the elements contained in the receiver are <= element. Does linear interpolation if the element is not contained but lies in between two contained elements. Note that the container holding the values must be sorted first
    	
----

[//]: # (keyword|operator_R_correlation)
### `R_correlation`
   Same signification as [corR](OperatorsBC#corR)
    	
----

[//]: # (keyword|operator_R_file)
### `R_file`

#### Possible use: 
  *  **`R_file`** (`string`) --->  `file` 

#### Result: 
Constructs a file of type R. Allowed extensions are limited to r
    	
----

[//]: # (keyword|operator_R_mean)
### `R_mean`
   Same signification as [meanR](OperatorsIM#meanR)
    	
----

[//]: # (keyword|operator_range)
### `range`

#### Possible use: 
  *  **`range`** (`int`) --->  `list`
  * `int` **`range`** `int` --->  `list`
  *  **`range`** (`int` , `int`) --->  `list`
  *  **`range`** (`int`, `int`, `int`) --->  `list` 

#### Result: 
Allows to build a list of int representing all contiguous values from zero to the argument. The range can be increasing or decreasing. Passing 0 will return a singleton list with 0
Allows to build a list of int representing all contiguous values from the first to the second argument, using the step represented by the third argument. The range can be increasing or decreasing. Passing the same value for both will return a singleton list with this value. Passing a step of 0 will result in an exception. Attempting to build infinite ranges (e.g. end > start with a negative step) will similarly not be accepted and yield an exception
Allows to build a list of int representing all contiguous values from the first to the second argument. The range can be increasing or decreasing. Passing the same value for both will return a singleton list with this value
    	
----

[//]: # (keyword|operator_rank_interpolated)
### `rank_interpolated`

#### Possible use: 
  * `container` **`rank_interpolated`** `float` --->  `float`
  *  **`rank_interpolated`** (`container` , `float`) --->  `float` 

#### Result: 
Returns the linearly interpolated number of elements in a list less or equal to a given element. The rank is the number of elements <= element. Ranks are of the form {0, 1, 2,..., sortedList.size()}. If no element is <= element, then the rank is zero. If the element lies in between two contained elements, then linear interpolation is used and a non integer value is returned. Note that the container holding the values must be sorted first
    	
----

[//]: # (keyword|operator_read)
### `read`

#### Possible use: 
  *  **`read`** (`string`) --->  `unknown` 

#### Result: 
Reads an attribute of the agent. The attribute's name is specified by the operand.

#### Examples: 
```
unknown 
agent_name <- read ('name'); //agent_name equals reads the 'name' variable of agent then assigns the returned value to the 'agent_name' variable. 

```
  
    	
----

[//]: # (keyword|operator_rectangle)
### `rectangle`

#### Possible use: 
  *  **`rectangle`** (`point`) --->  `geometry`
  * `float` **`rectangle`** `float` --->  `geometry`
  *  **`rectangle`** (`float` , `float`) --->  `geometry`
  * `point` **`rectangle`** `point` --->  `geometry`
  *  **`rectangle`** (`point` , `point`) --->  `geometry` 

#### Result: 
A rectangle geometry which side sizes are given by the operands.  

#### Comment: 
the center of the rectangle is by default the location of the current agent in which has been called this operator.the center of the rectangle is by default the location of the current agent in which has been called this operator.

#### Special cases:     
  * returns nil if the operand is nil.    
  * returns nil if the operand is nil.    
  * returns nil if the operand is nil.

#### Examples: 
```
 
geometry var0 <- rectangle(10, 5); // var0 equals a geometry as a rectangle with width = 10 and height = 5. 
geometry var1 <- rectangle({2.0,6.0}, {6.0,20.0}); // var1 equals a geometry as a rectangle with {2.0,6.0} as the upper-left corner, {6.0,20.0} as the lower-right corner. 
geometry var2 <- rectangle({10, 5}); // var2 equals a geometry as a rectangle with width = 10 and height = 5.

```
      


#### See also: 

[around](OperatorsAA#around), [circle](OperatorsBC#circle), [cone](OperatorsBC#cone), [line](OperatorsIM#line), [link](OperatorsIM#link), [norm](OperatorsNR#norm), [point](OperatorsNR#point), [polygon](OperatorsNR#polygon), [polyline](OperatorsNR#polyline), [square](OperatorsSZ#square), [triangle](OperatorsSZ#triangle), 
    	
----

[//]: # (keyword|operator_reduced_by)
### `reduced_by`
   Same signification as [-](OperatorsAA#-)
    	
----

[//]: # (keyword|operator_regression)
### `regression`

#### Possible use: 
  *  **`regression`** (`any`) --->  `regression` 

#### Result: 
Casts the operand into the type regression
    	
----

[//]: # (keyword|operator_remove_duplicates)
### `remove_duplicates`
   Same signification as [distinct](OperatorsDH#distinct)
    	
----

[//]: # (keyword|operator_remove_node_from)
### `remove_node_from`

#### Possible use: 
  * `geometry` **`remove_node_from`** `graph` --->  `graph`
  *  **`remove_node_from`** (`geometry` , `graph`) --->  `graph` 

#### Result: 
removes a node from a graph.  

#### Comment: 
all the edges containing this node are also removed.

#### Examples: 
```
 
graph var0 <- node(0) remove_node_from graphEpidemio; // var0 equals the graph without node(0)

```
  
    	
----

[//]: # (keyword|operator_replace)
### `replace`

#### Possible use: 
  *  **`replace`** (`string`, `string`, `string`) --->  `string` 

#### Result: 
Returns the String resulting by replacing for the first operand all the sub-strings corresponding the second operand by the third operand

#### Examples: 
```
 
string var0 <- replace('to be or not to be,that is the question','to', 'do'); // var0 equals 'do be or not do be,that is the question'

```
      


#### See also: 

[replace_regex](OperatorsNR#replace_regex), 
    	
----

[//]: # (keyword|operator_replace_regex)
### `replace_regex`

#### Possible use: 
  *  **`replace_regex`** (`string`, `string`, `string`) --->  `string` 

#### Result: 
Returns the String resulting by replacing for the first operand all the sub-strings corresponding to the regular expression given in the second operand by the third operand

#### Examples: 
```
 
string var0 <- replace_regex("colour, color", "colou?r", "col"); // var0 equals 'col, col'

```
      


#### See also: 

[replace](OperatorsNR#replace), 
    	
----

[//]: # (keyword|operator_restoreSimulation)
### `restoreSimulation`

#### Possible use: 
  *  **`restoreSimulation`** (`string`) --->  `int` 

#### Result: 
restoreSimulation
    	
----

[//]: # (keyword|operator_restoreSimulationFromFile)
### `restoreSimulationFromFile`

#### Possible use: 
  *  **`restoreSimulationFromFile`** (`ummisco.gama.serializer.gaml.GamaSavedSimulationFile`) --->  `int` 

#### Result: 
restoreSimulationFromFile
    	
----

[//]: # (keyword|operator_reverse)
### `reverse`

#### Possible use: 
  *  **`reverse`** (`msi.gama.util.GamaMap<K,V>`) --->  `container`
  *  **`reverse`** (`container<KeyType,ValueType>`) --->  `container`
  *  **`reverse`** (`string`) --->  `string` 

#### Result: 
the operand elements in the reversed order in a copy of the operand.  

#### Comment: 
the reverse operator behavior depends on the nature of the operand

#### Special cases:     
  * if it is a file, reverse returns a copy of the file with a reversed content    
  * if it is a population, reverse returns a copy of the population with elements in the reversed order    
  * if it is a graph, reverse returns a copy of the graph (with all edges and vertexes), with all of the edges reversed    
  * if it is a list, reverse returns a copy of the operand list with elements in the reversed order 
  
```
 
container var0 <- reverse ([10,12,14]); // var0 equals [14, 12, 10]
``` 

    
  * if it is a map, reverse returns a copy of the operand map with each pair in the reversed order (i.e. all keys become values and values become keys) 
  
```
 
map<int,string> var1 <- reverse (['k1'::44, 'k2'::32, 'k3'::12]); // var1 equals [44::'k1', 32::'k2', 12::'k3']
``` 

    
  * if it is a matrix, reverse returns a new matrix containing the transpose of the operand. 
  
```
 
container var2 <- reverse(matrix([["c11","c12","c13"],["c21","c22","c23"]])); // var2 equals matrix([["c11","c21"],["c12","c22"],["c13","c23"]])
``` 

    
  * if it is a string, reverse returns a new string with characters in the reversed order 
  
```
 
string var3 <- reverse ('abcd'); // var3 equals 'dcba'
``` 


    	
----

[//]: # (keyword|operator_rewire_n)
### `rewire_n`

#### Possible use: 
  * `graph` **`rewire_n`** `int` --->  `graph`
  *  **`rewire_n`** (`graph` , `int`) --->  `graph` 

#### Result: 
rewires the given count of edges.  

#### Comment: 
If there are too many edges, all the edges will be rewired.

#### Examples: 
```
 
graph var1 <- graphEpidemio rewire_n 10; // var1 equals the graph with 3 edges rewired

```
  
    	
----

[//]: # (keyword|operator_rgb)
### `rgb`

#### Possible use: 
  * `string` **`rgb`** `int` --->  `rgb`
  *  **`rgb`** (`string` , `int`) --->  `rgb`
  * `rgb` **`rgb`** `int` --->  `rgb`
  *  **`rgb`** (`rgb` , `int`) --->  `rgb`
  * `rgb` **`rgb`** `float` --->  `rgb`
  *  **`rgb`** (`rgb` , `float`) --->  `rgb`
  *  **`rgb`** (`int`, `int`, `int`) --->  `rgb`
  *  **`rgb`** (`int`, `int`, `int`, `float`) --->  `rgb`
  *  **`rgb`** (`int`, `int`, `int`, `int`) --->  `rgb` 

#### Result: 
Returns a color defined by red, green, blue components and an alpha blending value.

#### Special cases:     
  * It can be used with a name of color and alpha (between 0 and 255)    
  * It can be used with r=red, g=green, b=blue (each between 0 and 255), a=alpha (between 0.0 and 1.0)    
  * It can be used with r=red, g=green, b=blue (each between 0 and 255), a=alpha (between 0 and 255)    
  * It can be used with r=red, g=green, b=blue, each between 0 and 255    
  * It can be used with a color and an alpha between 0 and 255    
  * It can be used with a color and an alpha between 0 and 1

#### Examples: 
```
 
rgb var0 <- rgb ("red"); // var0 equals rgb(255,0,0) 
rgb var1 <- rgb (255,0,0,0.5); // var1 equals a light red color 
rgb var2 <- rgb (255,0,0,125); // var2 equals a light red color 
rgb var4 <- rgb (255,0,0); // var4 equals #red 
rgb var5 <- rgb(rgb(255,0,0),125); // var5 equals a light red color 
rgb var6 <- rgb(rgb(255,0,0),0.5); // var6 equals a light red color

```
      


#### See also: 

[hsb](OperatorsDH#hsb), 
    	
----

[//]: # (keyword|operator_rgb)
### `rgb`

#### Possible use: 
  *  **`rgb`** (`any`) --->  `rgb` 

#### Result: 
Casts the operand into the type rgb
    	
----

[//]: # (keyword|operator_rgb_to_xyz)
### `rgb_to_xyz`

#### Possible use: 
  *  **`rgb_to_xyz`** (`file`) --->  `list<point>` 

#### Result: 
A list of point corresponding to RGB value of an image (r:x , g:y, b:z)

#### Examples: 
```
 
list<point> var0 <- rgb_to_xyz(texture); // var0 equals a list of points

```
  
    	
----

[//]: # (keyword|operator_rms)
### `rms`

#### Possible use: 
  * `int` **`rms`** `float` --->  `float`
  *  **`rms`** (`int` , `float`) --->  `float` 

#### Result: 
Returns the RMS (Root-Mean-Square) of a data sequence. The RMS of data sequence is the square-root of the mean of the squares of the elements in the data sequence. It is a measure of the average size of the elements of a data sequence.
    	
----

[//]: # (keyword|operator_rnd)
### `rnd`

#### Possible use: 
  *  **`rnd`** (`float`) --->  `float`
  *  **`rnd`** (`int`) --->  `int`
  *  **`rnd`** (`point`) --->  `point`
  * `point` **`rnd`** `point` --->  `point`
  *  **`rnd`** (`point` , `point`) --->  `point`
  * `float` **`rnd`** `float` --->  `float`
  *  **`rnd`** (`float` , `float`) --->  `float`
  * `int` **`rnd`** `int` --->  `int`
  *  **`rnd`** (`int` , `int`) --->  `int`
  *  **`rnd`** (`float`, `float`, `float`) --->  `float`
  *  **`rnd`** (`point`, `point`, `float`) --->  `point`
  *  **`rnd`** (`int`, `int`, `int`) --->  `int` 

#### Result: 
a random integer in the interval [0, operand]  

#### Comment: 
to obtain a probability between 0 and 1, use the expression (rnd n) / n, where n is used to indicate the precision

#### Special cases:     
  * if the operand is a float, returns an uniformly distributed float random number in [0.0, to]    
  * if the operand is a point, returns a point with three random float ordinates, each in the interval [0, ordinate of argument]

#### Examples: 
```
 
float var0 <- rnd(3.4); // var0 equals a random float between 0.0 and 3.4 
int var1 <- rnd (2); // var1 equals 0, 1 or 2 
float var2 <- rnd (1000) / 1000; // var2 equals a float between 0 and 1 with a precision of 0.001 
float var3 <- rnd (2.0, 4.0, 0.5); // var3 equals a float number between 2.0 and 4.0 every 0.5 
point var4 <- rnd ({2.0, 4.0}, {2.0, 5.0, 10.0}); // var4 equals a point with x = 2.0, y between 2.0 and 4.0 and z between 0.0 and 10.0 
float var5 <- rnd (2.0, 4.0); // var5 equals a float number between 2.0 and 4.0 
point var6 <- rnd ({2.5,3, 0.0}); // var6 equals {x,y} with x in [0.0,2.0], y in [0.0,3.0], z = 0.0 
int var7 <- rnd (2, 4); // var7 equals 2, 3 or 4 
point var8 <- rnd ({2.0, 4.0}, {2.0, 5.0, 10.0}, 1); // var8 equals a point with x = 2.0, y equal to 2.0, 3.0 or 4.0 and z between 0.0 and 10.0 every 1.0 
int var9 <- rnd (2, 12, 4); // var9 equals 2, 6 or 10

```
      


#### See also: 

[flip](OperatorsDH#flip), 
    	
----

[//]: # (keyword|operator_rnd_choice)
### `rnd_choice`

#### Possible use: 
  *  **`rnd_choice`** (`list`) --->  `int` 

#### Result: 
returns an index of the given list with a probability following the (normalized) distribution described in the list (a form of lottery)

#### Examples: 
```
 
int var0 <- rnd_choice([0.2,0.5,0.3]); // var0 equals 2/10 chances to return 0, 5/10 chances to return 1, 3/10 chances to return 2

```
      


#### See also: 

[rnd](OperatorsNR#rnd), 
    	
----

[//]: # (keyword|operator_rnd_color)
### `rnd_color`

#### Possible use: 
  *  **`rnd_color`** (`int`) --->  `rgb`
  * `int` **`rnd_color`** `int` --->  `rgb`
  *  **`rnd_color`** (`int` , `int`) --->  `rgb` 

#### Result: 
rgb color
rgb color  

#### Comment: 
Return a random color equivalent to rgb(rnd(operand),rnd(operand),rnd(operand))Return a random color equivalent to rgb(rnd(first_op, last_op),rnd(first_op, last_op),rnd(first_op, last_op))

#### Examples: 
```
 
rgb var0 <- rnd_color(255); // var0 equals a random color, equivalent to rgb(rnd(255),rnd(255),rnd(255)) 
rgb var1 <- rnd_color(100, 200); // var1 equals a random color, equivalent to rgb(rnd(100, 200),rnd(100, 200),rnd(100, 200))

```
      


#### See also: 

[rgb](OperatorsNR#rgb), [hsb](OperatorsDH#hsb), 
    	
----

[//]: # (keyword|operator_rotated_by)
### `rotated_by`

#### Possible use: 
  * `geometry` **`rotated_by`** `float` --->  `geometry`
  *  **`rotated_by`** (`geometry` , `float`) --->  `geometry`
  * `geometry` **`rotated_by`** `int` --->  `geometry`
  *  **`rotated_by`** (`geometry` , `int`) --->  `geometry`
  *  **`rotated_by`** (`geometry`, `float`, `point`) --->  `geometry` 

#### Result: 
A geometry resulting from the application of a rotation by the right-hand operand angle (degree) to the left-hand operand (geometry, agent, point)
A geometry resulting from the application of a rotation by the right-hand operand angles (degree) along the three axis (x,y,z) to the left-hand operand (geometry, agent, point)  

#### Comment: 
the right-hand operand can be a float or a int

#### Examples: 
```
 
geometry var0 <- self rotated_by 45; // var0 equals the geometry resulting from a 45 degrees rotation to the geometry of the agent applying the operator. 
geometry var1 <- rotated_by(pyramid(10),45, {1,0,0}); // var1 equals the geometry resulting from a 45 degrees rotation along the {1,0,0} vector to the geometry of the agent applying the operator.

```
      


#### See also: 

[transformed_by](OperatorsSZ#transformed_by), [translated_by](OperatorsSZ#translated_by), 
    	
----

[//]: # (keyword|operator_round)
### `round`

#### Possible use: 
  *  **`round`** (`float`) --->  `int`
  *  **`round`** (`int`) --->  `int`
  *  **`round`** (`point`) --->  `point` 

#### Result: 
Returns the rounded value of the operand.

#### Special cases:     
  * if the operand is an int, round returns it

#### Examples: 
```
 
int var0 <- round (0.51); // var0 equals 1 
int var1 <- round (100.2); // var1 equals 100 
int var2 <- round(-0.51); // var2 equals -1 
point var3 <- {12345.78943,  12345.78943, 12345.78943} with_precision 2; // var3 equals {12345.79,12345.79,12345.79}

```
      


#### See also: 

[int](OperatorsIM#int), [with_precision](OperatorsSZ#with_precision), [round](OperatorsNR#round), 
    	
----

[//]: # (keyword|operator_row_at)
### `row_at`

#### Possible use: 
  * `matrix` **`row_at`** `int` --->  `list`
  *  **`row_at`** (`matrix` , `int`) --->  `list` 

#### Result: 
returns the row at a num_line (right-hand operand)

#### Examples: 
```
 
list var0 <- matrix([["el11","el12","el13"],["el21","el22","el23"],["el31","el32","el33"]]) row_at 2; // var0 equals ["el13","el23","el33"]

```
      


#### See also: 

[column_at](OperatorsBC#column_at), [columns_list](OperatorsBC#columns_list), 
    	
----

[//]: # (keyword|operator_rows_list)
### `rows_list`

#### Possible use: 
  *  **`rows_list`** (`matrix`) --->  `list<list>` 

#### Result: 
returns a list of the rows of the matrix, with each row as a list of elements

#### Examples: 
```
 
list<list> var0 <- rows_list(matrix([["el11","el12","el13"],["el21","el22","el23"],["el31","el32","el33"]])); // var0 equals [["el11","el21","el31"],["el12","el22","el32"],["el13","el23","el33"]]

```
      


#### See also: 

[columns_list](OperatorsBC#columns_list), 