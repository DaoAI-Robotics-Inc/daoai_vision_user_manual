Count Node
========================

Overview
----------

The Count node increases its counter every time the node has been run. This node is usually used in loop control.
The count is reset to 0 when the flowchart is reset.

.. image:: images/count/count_overview_1.png
	:align: center

.. image:: images/count/count_overview_2.png
	:align: center

|

Output
------------------

+-------------------------+-------------------+----------------------------------------------------------------------------------------------------------------------+
| Output                  | Type              | Description                                                                                                          |
+=========================+===================+======================================================================================================================+
| Count                   | int               | Number of time the count node has been run, note that the rest button on top of flowchart to reset the counter to 0. |
+-------------------------+-------------------+----------------------------------------------------------------------------------------------------------------------+

|

Node Settings
--------------

.. image:: images/count/count_node_settings.png
	:align: center

- **Reset Condition**:

    An expression that evaluates to a boolean.

- **Reset Value** (Default: 0):

    When Reset Condition is true, the Count node's count value is set to the Reset Value.

|

Procedure to Use
-----------------

1. Insert a Constant node, Count node.

.. image:: images/count/count_procedure_1.png
   :scale: 80%

2. Click the Constant node. Change the boolean field to True.

.. image:: images/count/count_procedure_2.png
   :scale: 80%

3. Click the Count node. Set the Reset Value to 9. 

.. image:: images/count/count_procedure_3.png
   :scale: 80%

4. Run the two nodes. You can see that the count changes from 0 to 9.

.. image:: images/count/count_procedure_4.png
   :scale: 80%