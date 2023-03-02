DA CloudNDepth Conv Node 
========================

Overview
-----------------

| Generate calibrated depth map image from point cloud input. 
| **DA CloudNDepth Conv** node is generally used when we need a calibrated depth image from point cloud to do 3D searching in nodes such as 3D Mod Finder, Metrology node, and Measurement node.  

.. image:: images/DA_CloudNDepth_conv/DA_CloudNDepth_Conv_overview_1.png
   :align: center

.. image:: images/DA_CloudNDepth_conv/DA_CloudNDepth_Conv_overview_2.png
   :align: center

Input and Output
-----------------

+----------------------------------------+-------------------------------+---------------------------------------------------------------------------------+
| Input                                  | Type                          | Description                                                                     |
+========================================+===============================+=================================================================================+
| Object                                 | Point Cloud                   | The point cloud data to be convert (From Camera etc.).                          |
+----------------------------------------+-------------------------------+---------------------------------------------------------------------------------+
| Depthmap Size X, Y                     | Int32                         | Size of the depth image x (width), y (height) dimension in pixels.              |
+----------------------------------------+-------------------------------+---------------------------------------------------------------------------------+
| Set Min. Size X, Y, Z                  | Double                        | Bounding box minimum x, y, z value.                                             |
+----------------------------------------+-------------------------------+---------------------------------------------------------------------------------+
| Set Max. Size X, Y, Z                  | Double                        | Bounding box maximum x, y, z value.                                             |
+----------------------------------------+-------------------------------+---------------------------------------------------------------------------------+

+-------------------------+-------------------+-------------------------------------------------------------------------------+
| Output                  | Type              | Description                                                                   |
+=========================+===================+===============================================================================+
| 8bit_depth              | Image             | 8 bit depth image.                                                            |
+-------------------------+-------------------+-------------------------------------------------------------------------------+
| cloud                   | cloud             | The input point cloud used for depth map conversion.                          |
+-------------------------+-------------------+-------------------------------------------------------------------------------+
| depth                   | Image             | 16 bit depth image composed of 8 bit grey scale image and 8-bit depth info.   |
+-------------------------+-------------------+-------------------------------------------------------------------------------+

Node Settings
-----------------
Source
~~~~~~~~~

.. image:: images/DA_CloudNDepth_conv/DA_CloudNDepth_Conv_node_settings_source.png

- **Object**:
   The point cloud data to be convert (From Camera etc.).

Depth Map Settings
~~~~~~~~~~~~~~~~~~

.. image:: images/DA_CloudNDepth_conv/node_setting.png

- **Depthmap Size X**:

   Size of the depth image x (width) dimension in pixels.

- **Depthmap Size Y**:

   Size of the depth image y (height) dimension in pixels.

Extraction Box Settings
```````````````````````

- **Set Min. Size**:

	- **X** : Bounding box minimum x value.
	- **Y** : Bounding box minimum y value.
	- **Z** : Bounding box minimum z value.

- **Set Max. Size**:

   	- **X** : Bounding box maximum x value.
	- **Y** : Bounding box maximum y value.
	- **Z** : Bounding box maximum z value.

Procedure to use
-----------------

1. We will also need a Camera node to demonstrate DA CloudNDepth Conv node. Right click insert node and insert a Camera node, and a DA CloudNDepth Conv node.
	.. image:: images/DA_cloudNdepth_conv/DA_CloudNDepth_Conv_procedure_insert_nodes.png
		:scale: 60%
    .. image:: images/DA_CloudNDepth_conv/DA_CloudNDepth_Conv_procedure_flowchart.png
        :scale: 90%

2. Here's a `link to tee.dcf file <https://daoairoboticsinc-my.sharepoint.com/:u:/g/personal/tzhang_daoai_com/EUaL8LFp-JlJugrB-VYSCr8BODvs7cyJszjIywupMCNDDg?e=XCPFjb>`_ for the camera input. Add a virtual Camera in the Platform Config and link the tee.dcf file as its input.
	.. image:: images/DA_cloudNdepth_conv/DA_CloudNDepth_Conv_procedure_camera_tee.png
		:scale: 80%

3. Link the source input to an appropriate node (eg. Camera or Cloud Process node). In this case, link to the pointCloud output of the previous Camera node.
	.. image:: images/DA_cloudNdepth_conv/node_steps_2.png
		:scale: 60%

4. Run the node and select a bounding box region that captures the area of interest.
	.. image:: images/DA_cloudNdepth_conv/node_steps_3.png
		:scale: 60%

5. If you see the following result which contains visible grid lines, you need to adjust the Depthmap Size X & Y dimensions to downsample your image until there are no visible grid lines.
	.. image:: images/DA_cloudNdepth_conv/node_steps_4_1.png
		:scale: 50%
	.. image:: images/DA_cloudNdepth_conv/node_steps_4_2.png
		:scale: 57%

|

Exercise
--------

Try to come up with the setting on **DA CloudNDepth Conv** node according to the requirements below. You can work on these exercise with the help of this article. We also have answers attached at the end of this exercise.
|
There is a project which requires the robot to pick all the occurrences of the T-tube in scene. 
Your colleague has setup the 3D camera and robot in the lab for experiment. 
Here's a `link to .dcf file <https://daoairoboticsinc-my.sharepoint.com/:u:/g/personal/tzhang_daoai_com/EUaL8LFp-JlJugrB-VYSCr8BODvs7cyJszjIywupMCNDDg?e=XCPFjb>`_ for the Camera input.

You need to help him setup the **DA CloudNDepth Conv** node in main_flowchart. Please choose the all correct answers from the options:

1. You are given a worskpace that has the camera and DA CloudNDepth Conv node set up, but you find that the result of DA CloudNDepth Conv is strange, as in the image below. How should you fix this?
	.. image:: images/DA_cloudNdepth_conv/node_exercise.png
		:scale: 70%

	A. Increase the X Y value in Extraction Box settings / Set Min. Size.
	B. Decrease the X Y value in Extraction Box settings / Set Max. Size.
	C. Decrease the X Y value in Deptmap Size X / Y. 
	D. Increase the X Y value in Deptmap Size X / Y. 

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

Answers for Exercises
------------------------

1. **Answer: C** (Decrease the X Y value in Deptmap Size X / Y)
	.. image:: images/DA_cloudNdepth_conv/node_answer.png
		:scale: 70%
**Explanation**: Recall in "Procedure to use" step 4, if you encouter the result containing grid lines, that means the width and height of the depthmap is too high.
Should reduce them accordingly to remove the gridlines.















