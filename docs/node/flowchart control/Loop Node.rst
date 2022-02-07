Loop Node
=========

Synopsis 
---------
	Node used to create a loop which executes until a break condition is met. 


Description 
---------
	Generates a sub-flowchart with a Break Node that gets iteratively executed until the condition defined in a Break Node (which can be the one generated upon placing the Loop Node, or by another Break Node placed by the user) evaluates to True. 

	 .. image:: images/loop_node.PNG
		:scale: 80%	
		
	The image above shows a Loop Node placed without any modifications. The Break Node is automatically inserted. 


Output 
---------
	Iteration:
		The number of times the loop has currently executed. Is reset to 0 every time the loop begins executing. 