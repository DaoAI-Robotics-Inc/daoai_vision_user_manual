Count Node
========================

Overview
------------

A counter node that increases its counter every time the node has been run, usually used in flowchart and loop control

Input and Output
------------------

+-------------------------+-------------------+-----------------------------------------------------------------------+
| Output                  | Type              | Description                                                           |
+=========================+===================+=======================================================================+
| count                   | Int               | Stores the number of times count node has been run                    |
+-------------------------+-------------------+-----------------------------------------------------------------------+

Settings
----------

.. image:: Images/count/setting.png

**Reset Condition**:
    Boolean value, evaluated from link or advanced expression, when evaluated to True, then the value of the counter will be reset.

**Reset Value** :
    The value for the counter node to reset to when reset flowchart, or Reset Condition is evaluated to True. 

Procedure to Use
------------------

1. Right click the node where you want to insert and insert an count pose node.
    .. image:: Images/count/step_1.png

2. You may optionally set Reset Condition and Reset Value.

3. You can access the Counter in other node like the folling image. (using Break node as an example)
    .. image:: Images/count/step_3.png



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