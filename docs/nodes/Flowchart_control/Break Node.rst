Break Node
===============

Overview
-------------------
The **Break Node** is used inside of a :ref:`Loop Node` to terminate the loop's execution. 
It has a single field 'Condition', which when evaluates to true, causes the loop which the **Break Node** is in to be broken out of. 

A **Break node** is automatically placed at the end of the sub-flowchart when inserting a Loop Node. 
A **Break node** cannot be inserted outside of a Loop.

.. image:: images/Break/break_overview_1.png
   :align: center

.. image:: images/Break/break_overview_2.png
   :align: center
		
|

Output 
-------------------

+-------------------------+-------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Output                  | Type              | Description                                                                                                                                       |
+=========================+===================+===================================================================================================================================================+
| Condition               | Bool              | When true, the loop which the Break Node is in will terminate. The execution will continue at the node after the loop node that is broken out of. |
+-------------------------+-------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+

|

Procedure to use
-------------------

1. Insert a Loop node.

.. image:: images/Break/break_procedure_1.png
   :scale: 80%	

|

2. A Break node is automatically inserted from the Loop node.

.. image:: images/Break/break_procedure_2.png
   :scale: 80%	

|

3. You can define the break condition with the Advance mode.

.. image:: images/Break/break_procedure_3.png
   :scale: 80%	

|

4. The loop stops executing when the Break condition is reached. The execution will continue at the node after the loop node that is broken out of.

.. image:: images/Break/break_procedure_4.png
   :scale: 80%	

|

