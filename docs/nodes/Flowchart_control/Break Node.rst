Break Node
===============

Overview
---------
	Node used inside of **For Loops** to terminate the loop's execution. 


Description 
-------------
	Has a single field 'Condition', which when evaluates to true, causes the For Loop which the Break Node is in to be broken out of. 

	 .. image:: images/break_node.png
		:scale: 80%	
		
	In this image we see a Break Node which was automatically placed at the end of the sub-flowchart in a Loop Node. 

	A break node can not be inserted outside of a For Loop.


.. Input 
.. ---------
.. 	Condition:
.. 		An expression which must evaluate to a boolean. When true, the loop which the Break Node is in will terminate. 


.. Output 
.. ---------
.. 	Condition:
.. 		The boolean value of the input Condition expression.

Function Signature
-----------------------
.. code-block:: cpp

	bool  Break( bool initial_value )


Input 
---------
+------------------------+---------+--------------+
| Input                  | Type    |  Description |
+========================+=========+==============+
| initial_value          | bool    | column 4     |
+------------------------+---------+--------------+
| body row 2             | ...     | ...          |
+------------------------+---------+--------------+


Output 
---------
+------------------------+------------+----------+----------+
| Header row, column 1   | Header 2   | Header 3 | Header 4 |
+========================+============+==========+==========+
| body row 1, column 1   | column 2   | column 3 | column 4 |
+------------------------+------------+----------+----------+
| body row 2             | ...        | ...      |          |
+------------------------+------------+----------+----------+

Procedure to use
-------------------
