Condition Node
=========

Synopsis 
---------
	Node used to execute either of two sub-flowcharts based on an inputted expression.


Description 
---------
	Has two sub-flowcharts and a single input, 'Condition'. When 'Condition' evaluates to True, the sub-flowchart corresponding to True is evaluated, when 'Condition' evaluates to False the sub-flowchart corresponding to False is evaluated. 
 .. image:: images/condition_node.PNG
	:scale: 80%	
	In this image we see a Condition Node serve to either go through a Pick Sort operation or to simply do nothing based off of the output from a Collision Avoidance Node. 


Input 
---------
	Condition:
		An expression which must evaluate to a boolean. When true, the sub-flowchart corresponding to True is evaluated, when false the sub-flowchart corresponding to False is evaluated. 


Output 
---------
	Condition:
		The boolean value of the input Condition expression. 