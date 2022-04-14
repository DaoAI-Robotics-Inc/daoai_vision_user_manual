3D Picking 
===========

For 3D picking, the previous detection procedure will detect the object positions in the point cloud coordinate, and the calibration procedure will detect the robot and camera relationship. The picking step is mapping what the camera detected to where to pick with the robot end effector. 

.. tip:: The camera and point cloud coordinate has a 180 degree rotation on the rx axis. 

Robot tool model
""""""""""""""""
one reference page (https://docs.pickit3d.com/en/latest/documentation/picking/robot-tool-model.html#robot-tool-model)

We are using the gripper node to define it with the tool model, and it will cover the tcp in flange part.

Pick points
""""""""""""""""
reference page (https://docs.pickit3d.com/en/latest/documentation/picking/pick-points.html#pick-points-detail). explain it with the gripper node. Also explain how to achieve the cylinder picking; Here will need to explain how to teach pose from real world as well.

Pick strategy
""""""""""""
Include the pick sort node config, and also include verification stacking checking ability

Collision prevention
""""""""""""

