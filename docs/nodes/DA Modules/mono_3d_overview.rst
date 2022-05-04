Overview 
================


Mono 3D node has 4 mode, accumulate, final, set_feature, and pose_estimation.
Normally, we use (accumulate + final) or set_feature to define object feature positions, and use pose_estimation to estimate pose

Define Object Features 
---------------------------

Features are some unique pattern on object that is easy to detect. We can construct the object if we know these feature points in 3d. 
To define the feature positoin, we can use set_feature mode, to direct input the 3d coordinates of feature points related to object origin.
	
We can also use (accumulate + final) mode to calculate the feature positions.
Initially accumulate node is empty, and every run of accumulate node will accumulate the data. There should be at least 4 captures for each feature. 
When the data are enough, we run final node, which will use the data in accumulate node to calculate the 3d coordinates of feature points related to object origin.


Pose Estimation 
--------------------------

Using the defined object feature positions and captured features from image, we estimate the pose for object, such that the average difference between [estimated feature position on image] and [actual captured feature position on image] is minimum.


Node Paramters 
------------------

	Accumulate:
		Mod Finder Result: 
			Comes from a 2d mod_finder, where we detect features from image.
		Pose: 
			The robot TCP_in_Base pose.
		Calibration Context: 
			A eye-in-hand calibration context, should be consistent with the input Pose.
		Image: 
			For visualizing.
	Final: 
		Reference Accumulate Node: 
			The accumulate Mono 3D Node where this node calculate data from.
		Name this file: 
			The name of file where node save the object feature positions. The file will be saved in the workspace directory.
	Set Feature:
		Set Feature Fields: 
			User-defined features.
		Name this file: 
			The name of file where node save the object feature positions. The file will be saved in the workspace directory.
	Pose Estimate:
		Mod Finder Result: 
			Comes from a 2d mod_finder, where we detect features from image.
		Pose: 
			The robot TCP_in_Base pose.
		Calibration Context: 
			A eye-in-hand calibration context, should be consistent with the input Pose.
		Name this file: 
			The name of file where node read the object feature positions. 
		Image: 
			For visualizing.


Output 
----------------

	Only Pose_Estimate mode has an output, which is a Vector<Pose> object.
	The pose object contains the object_in_camera pose. 

