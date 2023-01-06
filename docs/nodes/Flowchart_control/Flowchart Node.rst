Flowchart Node
=================

Overview
---------
The Flowchart node is used to nest a flowchart as a sub-flowchart in the flowchart the node is placed into. 
The Flowchart node Has a single input, 'Flowchart Name', which is the name of the other flowchart that is run when this node is executed. 

.. image:: images/Flowchart/flowchart_overview_1.png
   :align: center

.. image:: images/Flowchart/flowchart_overview_2.png
   :align: center

Upon placement of this node, you are prompted to select which flowchart the node should execute:

.. image:: images/flowchart_node_setup.png
   :scale: 50%	

In this example below using of a Flowchart Node, we see that upon a certain condition specific in the Switch Node, an entire flowchart would be run by just placing the single Flowchart Node.

.. image:: images/flowchart_node.png
   :scale: 80%	

|

Output 
---------

+-------------------------+-------------------+-----------------------------------------------------------------------------------+
| Output                  | Type              | Description                                                                       |
+=========================+===================+===================================================================================+
| FlowChartName           | string            | Name of the flowchart that runs when this node is executed.                       |
+-------------------------+-------------------+-----------------------------------------------------------------------------------+

|

Procedure to Use
-----------------

1. Add a new Flowchart from the top menu bar, and enter a name for the new flowchart.

.. image:: images/Flowchart/flowchart_procedure_1_1.png
   :scale: 90%	
.. image:: images/Flowchart/flowchart_procedure_1_2.png
   :scale: 80%	

|

2. Insert some nodes in the new flowchart for demonstration. 

.. image:: images/Flowchart/flowchart_procedure_2_1.png
   :scale: 116%	
.. image:: images/Flowchart/flowchart_procedure_2_2.png
   :scale: 80%	

|

3. Insert a Flowchart node in the main_flowchart.

.. image:: images/Flowchart/flowchart_procedure_3_1.png
   :scale: 80%	
.. image:: images/Flowchart/flowchart_procedure_3_2.png
   :scale: 80%	

|

4. Run the flowchart. You can see the print message from the new flowchart printed in the console.

.. image:: images/Flowchart/flowchart_procedure_4.png
   :scale: 90%	

|