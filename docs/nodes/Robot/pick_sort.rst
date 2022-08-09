Pick Sort
===========

Overview 
--------------------
	The Pick Sort node sorts the order for picking up objects according to different sorting types. Each type of sorting is based on a reference axis passed in(X, Y, Z). Depending on the preference from a user(ex. pick from the top first), it will output the order for pick up.

Input and Output 
--------------------
	
+----------------------------------------+-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Input                                  | Type                          | Description                                                                                                                                                                                           |
+========================================+===============================+=======================================================================================================================================================================================================+
| Poses Vect                             | vector<Pose>                  | A list of available poses of gripper to pick up objects. (Optional)                                                                                                                                   |                                   
+----------------------------------------+-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Object Vect                            | vector<Pose>                  | A list of objects that is able to be picked up. This is the parameter to be sorted.                                                                                                                   |
+----------------------------------------+-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Reference Axis                         | pose                          | The reference axis used to sort the picking order(Cloud Process Node).                                                                                                                                |
+----------------------------------------+-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Scene Cloud                            | cloud                         | The source point cloud.                                                                                                                                                                               |
+----------------------------------------+-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+



+-------------------------+-------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Output                  | Type              | Description                                                                                                                                                                                                          |
+=========================+===================+======================================================================================================================================================================================================================+
| sortedObjects           | vector<Pose>      | The output sorted list of objects for pick up.                                                                                                                                                                       |
+-------------------------+-------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| sortedOriginalIndices   | vector<Int>       | The mapping of the original indices and there new positions. For example if the original input is an array of size 5. This output may look like this [3, 1, 5, 2 0, 4] where the new index 0 is the original index 3.|
+-------------------------+-------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| sortedPoses             | vector<Pose>      | The output sorted list of gripper positions for pick up.                                                                                                                                                             |
+-------------------------+-------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Node Settings
---------------
	The following screen shots demonstrate the settings of the pick sort node.

Source Parameters
~~~~~~~~~~~~~~~~~

.. image:: images/pick_sort_1.png
	:scale: 100%

- **Poses Vect**: 

	A list of available poses of gripper to pick up objects. This input is optional and can be left empty and will be ignored.
    (Can use the output of the Collision Avoidance node)


- **Object Vect**: (Default value: 2000 ms) 

	A list of objects that is able to be picked up. This is the parameter that we use to sort by. If the Poses Vect is not left empty there must be a 1-to-1 correspondence between the poses and object.
    (Can use the output of the Collision Avoidance node)

- **Reference Axis**: 

	The reference axis used to sort the picking order. This can link to the Cloud Process Node using "Set Reference Frame" operation.

- **Scene Cloud**: 

	The source point cloud.

Pick Sort Setting
~~~~~~~~~~~~~~~~~

.. image:: images/pick_sort_2.png
	:scale: 100%

- **Sort Type**: (Default value: Highest Z)

	.. figure:: images/pick_sort_3.png
		:scale: 100%


	The order to sort the object positions and  poses for pick up in the reference coordinates. For example, if "Highest Z" is selected, the node will output the object positions and robot poses from the highest z value to the lowest z value.

- **Align Poses Orientation**: (Default value: None)

	.. figure:: images/pick_sort_4.png
		:scale: 100%

	This operation aligns the orientation of poses with the x-axis of the reference coordinates. 

	**0 degree**: the x-axis of objects align with the driection of the x-axis of the reference axis.
	For example, if the reference axis is set like the image below:

	.. figure:: images/pick_sort_8.png
		:scale: 100%

	The poses of the objects look like:

	.. figure:: images/pick_sort_9.png
		:scale: 100%	


	**toward reference axis**: the x-axis of objects point toward the origin of the reference axis.
	For example, if the reference axis is set like the image below:
	
	.. figure:: images/pick_sort_7.png
		:scale: 100%

	The poses of the objects look like:

	.. figure:: images/pick_sort_6.png
		:scale: 100%	

- **Lock Poses Z Direction**: (Default value: None)

	.. figure:: images/pick_sort_5.png
		:scale: 100%

	Fix the Z direction of object poses. For example, if "Positive" is selected, all of the poses will have positive Z relative with the z-axis of the reference axis. This feature is helpful when the target object is detected facing down, but it can only be approached from the top. This feature can make the objects all have positive/negative Z direction.

	
Procedure to use
~~~~~~~~~~~~~~~~



Exercise
~~~~~~~~

