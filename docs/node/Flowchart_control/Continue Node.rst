Constant Node
=========

Synopsis 
---------
	Node used inside of For Loops to forward loop execution to the next loop iteration. 


Description 
---------
	Has a single input, 'Condition', that when evaluates to True, forwards the execution of the loop that the node is in to the next loop iteration. This node allows the user to skip part of a For Loop sub-flowchart by simply going to the next iteration. 

	 .. image:: images/continue_node.PNG
		:scale: 80%	
		
	In this Loop Node, we see a Continue Node used to skip an Image Process operation when a condition is not met. 


Input 
---------
	Condition:
		An expression which must evaluate to a boolean. When true the loop which the Continue Node is in is forwarded to its next iteration.


Output 
---------
	Condition:
		The boolean value of the input Condition expression. 