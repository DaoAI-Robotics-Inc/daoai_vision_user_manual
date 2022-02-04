Switch Node
=========

Synopsis 
---------
	A generalization of the Condition Node to $\geq$ 2 cases used to execute one of many sub-flowcharts based on expressions for each case.


Description 
---------
	Upon placement, generates two sub-flowcharts, 'Case 1' and 'Default' although the user can then add as many other cases as required. Each case has an input 'Condition:case_X' which when evaluates to true, causes that case's sub-flowchart to be executed when the switch node is hit. If multiple cases have conditions which evaluate to True, the first case's sub-flowchart only will be executed (i.e. if Case 1 and Case 2 both have input conditions that evaluate to True, only Case 1's sub-flowchart would be executed). If no cases evaluate to True, the Default case's sub-flowchart will execute. 
 .. image:: images/switch_node.PNG
	:scale: 80%	
 .. image:: images/switch_node_exp.PNG
	:scale: 80%	
	The images above show a Switch Node could be used to switch between different calibration types. 


Input 
---------
	Condition\:case_X: 
		An expression which must evaluate to a boolean. When true, the sub-flowchart corresponding to this case is evaluated as long as no other conditions corresponding to cases of lower numbers also evaluate to True. 


Output 
---------
	Condition\:case_X:
		The boolean value of the input Condition expression. 