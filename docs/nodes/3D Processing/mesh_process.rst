Mesh Process Node
============================

Overview
--------------------

Often, polygon meshes contain sparse points, relying more on polygons to represent surfaces. 
The Mesh Process Node processes an input polygon mesh and generates a point cloud that can be used for finding model features.

.. image:: Images/mesh_process/mesh_process_overview_1.png
   :align: center

.. image:: Images/mesh_process/mesh_process_overview_2.png
   :align: center

.. image:: Images/mesh_process/mesh_process_overview_3.png
   :align: center

Input and Output
--------------------

+-------------------------+-------------------+------------------------------------------------------------------------+
| Input                   | Type              | Description                                                            |
+=========================+===================+========================================================================+
| Model Mesh              | Mesh              | A polygon mesh for the model (.ply).                                   |
+-------------------------+-------------------+------------------------------------------------------------------------+
| Process                 | Int32             | The type of mesh processing performed.                                 |
+-------------------------+-------------------+------------------------------------------------------------------------+

+-------------------------+-------------------+------------------------------------------------------------------------+
| Output                  | Type              | Description                                                            |
+=========================+===================+========================================================================+
| cloud                   | Cloud             | point cloud or edge cloud converted from polygon mesh.                 |
+-------------------------+-------------------+------------------------------------------------------------------------+
| mass center             | Point4f           | The mass center of the resulting point cloud.                          |
+-------------------------+-------------------+------------------------------------------------------------------------+

Node Settings
----------------

Data Source
~~~~~~~~~~~~

.. image:: Images/mesh_process/mesh_process_data_source.png
   :align: center

Process Settings
~~~~~~~~~~~~~~~~

.. image:: Images/mesh_process/mesh_process_process_settings.png
   :align: center

- Process Type
   The type of mesh processing performed. Select from one of "Generate Cloud" or "Generate Edge".
      - Generate Cloud: Generates a dense cloud of the mesh's surface. 
      - Generate Edge: Generates a point cloud with the mesh's edges. Recommended for flat objects.

Along with Edge Extract Node and the Use Edge setting in the Scene Match Node.

.. image:: Images/mesh_process/cloud.png
   :align: center

.. image:: Images/mesh_process/edge.png
   :align: center

|

Procedure to Use
----------------

1. Insert a Reader, and a Mesh Process node.

2. In the Reader node, read a mesh file. `Here <>`_ is a mesh file if you need one.

3. In the Mesh Process node, link to the Reader's ____ output.

4. You can visualize the output by checking the checkboxes beside the display window.

5. Select Generate Edge and run the node.

6. Select Generate Cloud and run the node.

|

Exercise
--------------------------------------





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
--------------------------------------