Overview
=======================

Input
--------------------------------

* Dimensions: a vector of box dimensions from the output of box volume estimation node
* Original Poses: a vector of poses representing the pick pose of each box
* Pose Order (optional): a vector representing the order of the orignal poses from the pick sort node

Output
--------------------------------

* newPoses: valid poses where the vaccum could suck up the orignal box

Parameters
------------------------------------

* Plate X: width of the picking plate, default is 300mm
* Plate Y: height of the picking plate, default is 300mm
* Threshold low: how much of the box should be covered to be picked up, default is 0.5
* Threshold high: the upper bound of box coverage to be picked up, default is 1
* Pre Sort Poses: sort poses in a back-and-force moving pattern, as shown in the below image, the ordering of the pose follows a z-shape pattern.