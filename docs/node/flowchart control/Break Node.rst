Break Node
=========

Synopsis 
---------
	Node used inside of For Loops to terminate the loop's execution. 


Description 
---------
	Has a single field 'Condition', which when evaluates to true, causes the For Loop which the Break Node is in to be broken out of. 
 .. image:: images/break_node.PNG
	:scale: 80%	
	In this image we see a Break Node which was automatically placed at the end of the sub-flowchart in a Loop Node. 


Input 
---------
	Condition:
		An expression which must evaluate to a boolean. When true, the loop which the Break Node is in will terminate. 


Output 
---------
	Condition:
		The boolean value of the input Condition expression.