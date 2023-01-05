Halt Node
=========

Overview
---------
Halt node is used to stop a flowchart's execution. 

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

+-------------------------+-------------------+-----------------------------------------------------------------------------------+
| Output                  | Type              | Description                                                                       |
+=========================+===================+===================================================================================+
| Halt                    | Bool              | When true the execution of the flowchart is halted at this node.                  |
+-------------------------+-------------------+-----------------------------------------------------------------------------------+

Procedure to Use
-----------------

1. Insert a Print node, and a Halt node.

.. image:: images/Halt/halt_procedure_1.png
   :scale: 100%	

|

2. Click the Print node, enter "hello" as the print message.

.. image:: images/Halt/halt_procedure_2.png
   :scale: 100%	

|

3. Click the Halt node, change the Halt value to True.

.. image:: images/Halt/halt_procedure_3.png
   :scale: 100%	

|

4. Run the flowchart. You can see the message "hello" once in the console, and the flowchart is stopped by the Halt node. 

.. image:: images/Halt/halt_procedure_4.png
   :scale: 100%	

|
