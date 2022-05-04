Setup the Robot TCP
=================

Setting up the TCP for the system is important for the Teach_Pose process. According to the real robot, different gripper has different pose to approach the object. 

Note that: 2D Picking should use a pencil and plane gripper mesh, pencil can easily visualizing the X and Y coordinates of the reference point; plane can visualizing the Z coordinate.

Gripper mesh is loaded from the ``Reader`` Node. ``Gripper`` Node can visualize the gripper mesh in scene. In sample template, virtual robot is used; therefore, you might need to adjust the gripper pose manually to align the gripper mesh with object. 
If using real robot, the ``Gripper`` visualization is adjusted with real robot. For detail please see :ref:`2D Picking: Teach Pose<2D Picking Teach Pose>` , :ref:`3D RGB Picking: Teach Pose<3D RGB Picking Teach Pose>` , :ref:`3D Depth Picking: Teach Pose<3D Depth Picking Teach Pose>` .

Note: in 2D Picking, we align the pencil with the plane, there is no real world scene in this ``Gripper`` .

.. image:: Images/2d_gripper.png
    :align: center
    
|

