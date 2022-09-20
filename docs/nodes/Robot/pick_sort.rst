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

1. Take an image

.. image:: images/1.png
	:scale: 70%

2. Set the reference Frame

.. image:: images/2.png
	:scale: 70%

3. Detect 3D position of objects.

.. image:: images/3.png
	:scale: 70%

.. image:: images/4.png
	:scale: 70%

4. Run the pick sort node. This is set to sort by the highest Z with a "Align Poses Orientation" of 90 degree.

.. image:: images/5.png
	:scale: 60%

Pick Strategy 
--------------------

In this section, we will be talking about how to apply some other nodes/functionalities to alter the picking strategies. 
There are 3 strategies can be applied to our picking pose:

    #. Picking objects with designated orders;
    #. Altering the picking rotations for objects;
    #. Limiting the tilt of picking poses;

Object Orders
~~~~~~~~~~~~~~

We will be using our **RGB Mod Finder** template as our example. This section we will skip the details of **Detection** flowchart, you can check out `this article <https://daoai-robotics-inc-daoai-vision-user-manual.readthedocs-hosted.com/en/latest/complete-vision-guidance/detection/mod-finder/mod-finder-overview.html>`_ for knowledge about **Detection**. 

.. image:: Images/tee.png
    :align: center

|

In the image above, you can see there are 8 objects in scene. For industrial productivity, 
time is valuable for factories. Therefore, picking multiple objects within **one image capture** is usually required. 
When thinking about more complex industrial environment and requirements, objects might stack on one and another. 
Solution to such problems is to sort the pickable objects then picking them one by one(if using one robot). 
Increasing the amount of robots can be also helpful, but note that robots might have potential collision when 2 or more robots are working in the same area. 
We will discuss about this in the later section of this article **Collision Prevention**. 

.. image:: Images/ind_objs.png
    :align: center

|

**Pick Sort** is the node which sorts the pick poses.

.. image:: Images/pick_sort.png
    :align: center

Linking all the inputs for **Pick Sort** node, then you can use the the pick sort setting to sort the poses. 

.. image:: Images/pick_sort_config.png
    :align: center

You choose the orders which sorts the poses. **Highest Z** represents the poses will be sorted in decreasing order of Z value. The output of **Pick Sort** node 
is a vector of poses which ordered from highest Z to lowest Z. 

.. image:: Images/sorted_tees.png
    :align: center

Now the poses have sorted and you can see the label of these objects. **1** will be the first object to be picked, then 
**2** and so on. This feature is 
useful especially when encountering the stacking and overlapping objects like image shown below. 

.. image:: Images/sorted_detectors.png
    :align: center

|

Pick Pose Rotations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Continue from **Object Orders**, you can see that the smoke detector is circle shape object, the any pick pose rotates from Z-axis will the providing the 
same pick pose in real life. But note that, robot is not human, they don't know if the pose can be rotates in any directions or angles. The robot will 
perform picking with the pose's x, y, z, rx, ry, rz values. 

.. image:: Images/rz.png
    :align: center

Therefore, in concern of efficiency, we should ask the robot to ignore the rz rotation and pick all the objects no matter which rz values they have.

You can see that the **Pick Sort** node has a setting called **Align Poses Orientation**. 
This setting is able to change the sorted poses with same rotations. It can help you to align all the sorted poses with same x, y direction.

.. image:: Images/align_poses_Orientation.png
    :align: center
|

There are several degrees you can align these poses to: 0, 90, 180, 270 and towards reference frame:

.. image:: Images/degrees.png
    :align: center

|

As it states from the options, the poses will rotate to such a degree. 

.. image:: Images/rotation.png
    :align: center

|

Another way to alter the pick pose rotation is the  **Gripper** node. You can change the relation of **Object -> Tool** (or **Tool -> Object**, depending on how you build your 
**Transformation Tree** node). This relation has flexibility between gripper and object. By default, the relation is defined from your teach pose(**Robot Read**) or the value you input for virtual Pose Define process(like the image shown below). 

.. image:: Images/default_pose_gripper.png
    :align: center

You can use this flexibility to enable pick pose rotation on Z-axis: 

.. image:: Images/pick_pose_rotation_gripper.png
    :align: center

You can use this setting to allow the Tool picking with rotation at Z-axis no more than  180 degree or even full circle. This can achieve the same purpose like above using **Pick Sort** node rotation. 

.. image:: Images/z-rotation.png
    :align: center

|

Pick Pose Tilting
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In real world environment, objects tilt will always happen. If the objects are within an area with potential collision, sometime you might need to apply the tilting on 
poses in order to perform picking. 

.. image:: Images/tilting_gripper.png
    :align: center
|

For example, the smoke detector with **red circle** is located closely to the edge of the basket. When **Vision** calculates the pick pose for this object, 
it is usually perpendicular to the object surface(it can be changed to perpendicular to the reference frame's axises as well, let's pretend the pick pose is 
perpendicular to object surface now). And if the robot is trying to pick this detector with this pick pose(indicated with **yellow line**), the robot arm is possibly 
going to collide with the edge of the basket. 

In this case, applying 20-30 degree of tilt to the pick pose is still able to pick up the detector, and the robot is collision-free. Therefore, allowing 
proper amount of tilting is helpful. 

.. image:: Images/gripper_tilting_setting.png
    :align: center

|

    * Tile Axis is the setting of which axis/axises you allow this pose to tilt. You can tilt it with x & y axises, x-axis or y-axis.
    * The Tilt Angle is maximum angle you allow the pose to rotate.
    * Pick Strategy is the preference of this picking pose: **Pick from Top** or **Pick with Less Tilt**




Exercise
--------------------
TODO