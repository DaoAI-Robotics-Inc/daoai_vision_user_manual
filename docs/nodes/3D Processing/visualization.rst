Visualize Node
============================

Overview
-------------
The Visualize node is a utility node that visualizes point clouds or meshes. It can also apply poses to objects before visualizing.

The visualize node takes in an object (either point cloud or mesh) and the pose (affine3f optional). It does not output anything, it only uses the display.

.. image:: Images/visualize/visualize_overview_1.png
   :align: center

.. image:: Images/visualize/visualize_overview_2.png
   :align: center

.. image:: Images/visualize/visualize_overview_3.png
   :align: center

Input and Output
---------------------------

+-------------------------+--------------------+------------------------------------------------------------------------+
| Input                   | Type               | Description                                                            |
+=========================+====================+========================================================================+
| Object                  | Point Cloud / Mesh | The object to be visualized.                                           |
+-------------------------+--------------------+------------------------------------------------------------------------+
| Object Pose             | Pose               | The pose to be applied to the object (optional).                       |
+-------------------------+--------------------+------------------------------------------------------------------------+
| Show Axis               | bool               | Whether to display the pose's axis or not.                             |
+-------------------------+--------------------+------------------------------------------------------------------------+
| Show Object             | bool               | Whether to display the object or not.                                  |
+-------------------------+--------------------+------------------------------------------------------------------------+
| Axis Scale              | int                | The size of the axis to be shown.                                      |
+-------------------------+--------------------+------------------------------------------------------------------------+

The Visualize node has no output, it only uses the display.

Run the node or click "Visualize All" to display the objects.

Node Settings
---------------------------

Visualizations
~~~~~~~~~~~~~~~

.. image:: Images/visualize/visualize_node_settings_visualizations.png
   :align: center

There can be an arbitrary number of visualization items.

- Object
   The object to be visualized.

- Object Pose
   The pose to be applied to the object (optional).

- Show Axis (Default: false)
   Whether to display the pose's axis or not.

- Show Object (Default: true)
   Whether to display the object or not.

- Axis Scale (Range: [1,100]; Default: 50)
   The size of the axis to be shown.

Procedure to Use
---------------------------
We will need a few more nodes to demonstrate the Visualize node. You can get the files `here <>`_ .

1. Insert a Calibration, Transformation Tree, 2 Readers, and Visualize node.
    .. image:: Images/visualize/visualize_procedure_1.png
       :align: center

2. In Calibration, select Load mode, and input the calibration file name. Make sure the file is stored in the project's calibrations folder. 
    .. image:: Images/visualize/visualize_procedure_2.png
       :align: center

3. In the Transformation Tree, we need the tool in cloud relation to visualize the gripper. Add a tool in base relation, and link the bag's output pose; Add a cam in base relation, and link calibration's camInBase output; Add a cam in cloud relation, click "Set Pose", change Rot a to 180. Finally, add a tool in cloud output.
    .. image:: Images/visualize/visualize_procedure_3_1.png
       :align: center

4. In the first Reader node, read the gripper's mesh file.
    .. image:: Images/visualize/visualize_procedure_4.png
       :align: center

5. In the second Reader node, read the bag file.
    .. image:: Images/visualize/visualize_procedure_5.png
       :align: center

6. In the Visualize node, click "Add Viz" to add a visualization (Viz_0). For Object, link the first reader's outputMesh (gripper). For Object Pose, link the Transformation Tree's output.
    .. image:: Images/visualize/visualize_procedure_6.png
       :align: center

7. Click "Add Viz" to add another visualization (Viz_1). For Object, link the second reader's bag cloud output. You can leave Object Pose empty as the object is the scene.
    .. image:: Images/visualize/visualize_procedure_7.png
       :align: center

8. Run the flowchart, and click on Visualize node. You can see the scene and gripper are displayed.
    .. image:: Images/visualize/visualize_procedure_8.png
       :align: center
|

Exercise
---------------------------
You have this flowchart and are trying to see the visualization of the scene with the gripper. However, when you click on the Visualize node, the display is a black screen. How can you fix the problem, given the following visualizations settings?

.. image:: Images/visualize/visualize_exercise_1.png
   :align: center

|
|
|
|
|
|
|
|
|
|
|
|
|
|
|

Answers for Exercise
---------------------------
1. The black screen is due to the wrong box option selected. "Show Object" needs to be selected to display.

