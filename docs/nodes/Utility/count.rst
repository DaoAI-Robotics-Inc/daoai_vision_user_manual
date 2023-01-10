Count Node
========================

Overview
----------

The Count node increases its counter every time the node has been run. This node is usually used in loop control.

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

Node Settings
--------------

.. image:: images/count/count_node_settings.png
	:align: center

- **Reset Condition**:

    An expression that evaluates to a boolean.

- **Reset Value** (Default: 0):

    When Reset Condition is true, the Count node's count value is set to the Reset Value.

