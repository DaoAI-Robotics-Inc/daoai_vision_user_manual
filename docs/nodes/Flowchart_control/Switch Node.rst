Switch Node
=============

Overview
---------

A generalization of the Condition Node to at least 2 cases used to execute one of many sub-flowcharts based on expressions for each case.
Upon placing a Switch node, generates two sub-flowcharts, 'Case 1' and 'Default'.
Each case has an input 'Condition: case_x' which when evaluates to true, causes that case's sub-flowchart to be executed when the switch node is hit. 
If multiple cases have conditions evaluate to True, then the first case's sub-flowchart will be executed (i.e. if Case 1 and Case 2 both have input conditions that evaluate to True, only Case 1's sub-flowchart would be executed). 
The Default case's sub-flowchart will execute when all other cases are evaluated to false.

.. image:: images/switch_node.png
	:scale: 80%	

.. image:: images/switch_node_exp.png
	:scale: 80%	
		
The images above show a Switch Node could be used to switch between different calibration types. 


Input 
---------
Condition\: case_x: 
	An expression which must evaluate to a boolean. 
	When true, the sub-flowchart corresponding to this case is evaluated as long as no other conditions corresponding to cases of lower numbers also evaluate to True. 


Output 
---------

+-------------------------+-------------------+-----------------------------------------------------------------------------------+
| Output                  | Type              | Description                                                                       |
+=========================+===================+===================================================================================+
| Condition: case_x       | bool              | The boolean value of the input Condition expression.                              |
+-------------------------+-------------------+-----------------------------------------------------------------------------------+

Procedure to Use
-----------------

1. Set up the flowchart as in the following image.

.. image:: images/Switch/switch_procedure_1.png
   :scale: 80%	

|

2. Click the Constant node. Change the Int Field to 2.

.. image:: images/Switch/switch_procedure_2.png
   :scale: 80%	

|

3. Click the Switch node, select case_2 and Advanced mode. Let condition: case_2 evaluates to True when the Constant Int is 2.

.. image:: images/Switch/switch_procedure_3.png
   :scale: 80%	

|

4. Click the Print node. Type a print message.

.. image:: images/Switch/switch_procedure_4.png
   :scale: 80%	

|

5. Click the Halt node. Set the Halt value to True.

.. image:: images/Switch/switch_procedure_5.png
   :scale: 80%	

|

6. Run the flowchart. You can see the print message from Case 2, and the flowchart is halted.

.. image:: images/Switch/switch_procedure_6.png
   :scale: 80%	

|

Exercise
---------
1. Given there are case_1, case_2, case_3, and case_default. If both case_2 and case_default are both true, which case is run?

A. case_1
B. case_2
C. case_3
D. case_default

|
|
|
|
|
|
|
|
|
|
|
|
|
|
|

Answers for Exercise
-----------------------
1. B. case_2 is run. 