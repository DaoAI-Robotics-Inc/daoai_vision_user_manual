Overview
=======================

The Pose Generation node is responsible to generate multiple poses for the robot (gripper pose inside the base coordinates) that can be used for calibration.

Three moving types are available:

* Circle
* Square
* Trapezoid


Input
--------------------

* Ref Gripper To Base: (DataType: Pose)A Homogeneous matrix that has the initial pose of the gripper that will be used in order to generate the other poses.

* Camera To Gripper: (DataType: Pose)A Homogeneous that could have an initial estimate for the relationship between the camera and the gripper (or the calibration board and the gripper if the Eye-To-Hand configuration is being used). If unknown, an identity matrix is set.

Output
----------------------

* poses: (DataType: vector<Pose>) a vector of generated poses