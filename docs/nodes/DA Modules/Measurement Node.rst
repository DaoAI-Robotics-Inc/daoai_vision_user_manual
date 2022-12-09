Measurement Node 
==================

Overview
--------------------
The Measurement node is used to find and measure edge, circle, stripe on a gray image.

.. image:: images/Measurement/measurement_node_overview_1.png
   :align: center

.. image:: images/Measurement/measurement_node_overview_2.png
   :align: center

Inputs and Outputs
--------------------

+----------------------------------------+-------------------------------+---------------------------------------------------------------------------------+
| Input                                  | Type                          | Description                                                                     |
+========================================+===============================+=================================================================================+
| Image                                  | png                           | The gray image to be measured. (from Camera, Reader etc.)                       |
+----------------------------------------+-------------------------------+---------------------------------------------------------------------------------+
| Use Reference Frame                    | String                        | The name of the mod finder node to use the reference frame from.                |
+----------------------------------------+-------------------------------+---------------------------------------------------------------------------------+
| Show Interactive Display               | bool                          | Whether Interactive Display is used.                                            |
+----------------------------------------+-------------------------------+---------------------------------------------------------------------------------+

+-------------------------+---------------------+------------------------------------------------------------------------+
| Output                  | Type                | Description                                                            |
+=========================+=====================+========================================================================+
| results                 | MapSMeasResultData  | The measurement results.                                               |
+-------------------------+---------------------+------------------------------------------------------------------------+

 .. image:: images/Measurement/measurement_0.JPG
	:scale: 60%

Node Settings
--------------------

Data Source
```````````````````
.. image:: images/Measurement/measurement_node_settings_data_source.png
   :align: center

- **Image**:
     - The gray image to be measured. (from Camera, Reader etc.)

Region Settings
```````````````````
- **Use Reference Fixture**:
    - The name of the Mod Finder node to use the reference frame (optional). Please refer to :ref:`Reference Fixture System` for more information.

- **Show Interactive Display**:
    - Can edit markers after clicking “Show Interactive Display”.


Markers Parameters
```````````````````

.. image:: images/Measurement/measurement_edge_edit.png
   :align: center


.. image:: images/Measurement/measurement_stripe_edit.png
   :align: center


.. image:: images/Measurement/measurement_circle_edit.png
   :align: center

- **Number of Occurences** (Default: 1):
   The number of maximum markers to detect.

- **Min Occurances** (Default: -1):
   The minimum number of markers to detect. If fewer marker is detected than the min occurances, then it is a detection fail.

Circle Marker Fields

.. image:: images/Measurement/measurement_circle_marker_fields.png
   :align: center

- **Polarity** (Default: Any):
   The polarity of edge to detection direction. Positive is from black to white, Negative is from white to black.

- **Max Association Distance** (Default: 0):
   Not range limit, unit is pixel. 
   The maximum distance between a marker’s edge (either straight or circular) and its associated sub-edges during fit operation.
   For edge and stripe markers, it is measured perpendicular from the fitted edge position, along to the search direction.
   For circle markers, it is measured radially from the fitted circle perimeter.


- **Min Edge Value** (Default: 10):

Ring Region Fields

.. image:: images/Measurement/measurement_ring_region_fields.png
   :align: center

- **Enable Clipping** (Default: false):
   Whether to apply a clipped search region to search the marker. Useful when search region includes region outside of the image.

- **Center X, Center Y**:
   The coordinates of the Ring Region, measured from the center.

- **Inner Radius, Outer Radius**:
   Size of the ring region.

Edge Marker Fields

- **Polarity** (Default: Any):
   The polarity of edge to detection direction. Positive is from black to white, Negative is from white to black.

- **Max Association Distance** (Default: 0):
   Not range limit, unit is pixel. 
   The maximum distance between a marker’s edge (either straight or circular) and its associated sub-edges during fit operation.
   For edge and stripe markers, it is measured perpendicular from the fitted edge position, along to the search direction.
   For circle markers, it is measured radially from the fitted circle perimeter.

- **Min Edge Value** (Default: 2):


Stripe Marker Fields

.. image:: images/Measurement/measurement_stripe_marker_fields.png
   :align: center

- **Polarity** (Default: Any):
   The polarity of edge to detection direction. Positive is from black to white, Negative is from white to black.

- **Polarity 2** (Default: Opposite):
   Only available for stripe markers. Decides the polarity of the second edge of stripe, related to stripe’s first edge.

- **Max Association Distance** (Default: 0):
   Not range limit, unit is pixel. 
   The maximum distance between a marker’s edge (either straight or circular) and its associated sub-edges during fit operation.
   For edge and stripe markers, it is measured perpendicular from the fitted edge position, along to the search direction.
   For circle markers, it is measured radially from the fitted circle perimeter.

- **Min Edge Value** (Default: 10):
   

Box Region Fields

.. image:: images/Measurement/measurement_box_region_fields.png
   :align: center

- **Marker Orientation** (Default: Vertical):
   Direction of the edge to be detected.

- **Enable Clipping** (Default: false):
   Whether to apply a clipped search region to search the marker. Useful when search region includes region outside of the image.

- **Enable Multi Angle** (Default: false):

- **Center X, Center Y**:
   The coordinates of the Ring Region, measured from the center.

- **Width, Height**:
   The size of the box region.



Procedure to Use
--------------------
We will need a few more nodes to demonstrate the usage of Measurement node.
Insert Camera, (2D) Mod Finder, and Measurement node.

Set up the tee.dcf scene in the Camera.
In Mod Finder, link the Camera's image output.
Run the Mod Finder node, and define a model on the image. Then define a Reference Point for the model.

1. Insert a Reader node. You may use the data `here <https://daoairoboticsinc-my.sharepoint.com/:u:/g/personal/xchen_daoai_com/ETnjM6E8D89FsYDUfeMeBIUBSBxAuxVoCqcmJZMgbIYKdg?e=l4fBZ3>`_.  Read from this folder.

.. image:: images/Measurement/measurement_procedure_1.png
   :scale: 60%

2. Insert a 2D Mod finder. Define the object as the fixture. You might want to read :ref:`Reference Fixture System` for more information. 

.. image:: images/Measurement/measurement_mod_finder_fixture_1.png
   :scale: 55%

.. image:: images/Measurement/measurement_mod_finder_fixture_2.png
   :scale: 100%

3. Insert a Measurement node. Uses the Mod Finder node in step 2 as the Reference Fixture Node.

.. image:: images/Measurement/measurement_procedure_3.png
   :scale: 80%

4. Enable "Show Interactive Display". Then click '+', choose a marker type, click "Start Drawing New Region" to add markers. Click "Stop Drawing New Region" after you finished drawing the marker. In this case, we will draw a Circle Marker.

.. image:: images/Measurement/measurement_procedure_4_1.png
   :scale: 76%

.. image:: images/Measurement/measurement_procedure_4_2.png
   :scale: 60%

5. Run the flowchart, the Measurement node will find the feature using the reference fixture from Mod Finder.

.. image:: images/Measurement/measurement_procedure_5_1.png
   :scale: 85%

.. image:: images/Measurement/measurement_procedure_5_2.png
   :scale: 60%


6. In Quick Evaluate, type the marker's name in marker[''] to check its evaluated results. In this case, the circle marker is named "Circle_Marker_Region_1" and we can check the circle's radius, x, and y values by typing in the circle marker's name. You can see the circle's radius under the Evaluated Value column.

.. image:: images/Measurement/measurement_procedure_6_1.png
   :scale: 80%

.. image:: images/Measurement/measurement_procedure_6_2.png
   :scale: 80%

Exercise
--------------------
1. What would be a good marker for measuring the width of this region?

2. What is the approriate settings for detecting this region?

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

Answers to Exercise
--------------------

