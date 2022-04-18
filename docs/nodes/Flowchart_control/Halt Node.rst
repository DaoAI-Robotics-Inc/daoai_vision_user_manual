Halt Node
=========

Synopsis 
---------
	Node used to halt flowchart execution. 


Description 
---------
	Halts flowchart execution until the node input 'Halt' expression evaluates to False.

	 .. image:: images/halt_node.png
		:scale: 80%	
		
	In this example of a Halt Node in use, we see that it would halt execution until the linked Mod Finder V2 Node has executed successfully. 

Input 
---------
	Halt:
		An expression which must evaluate to a boolean. When true the execution of the flowchart is halted at this node. 


Output 
---------
	Halt:
		The boolean value of the input Halt expression. 