Procedure of Using This Node
==============================

Define Features:
	1. Run eye-in-hand calibration, get eye-in-hand calibration context
	2. Define at least 4 features on object by 2d mod_finder node.
	3. From different positions, capture this object and use 2d mod_finder node to find its feature, and run accumulate mode node to accumulate data. each feature on object should be captured at least 4 times.
	4. run final mode node to calculate the position of feature relative to object.

Set Feature:
	As an alternative way of define features, user may input the feature_in_object using position vallues

Pose Estimate:
	0. run eye-in-hand calibration, get calibration context. 
	1. caprure object, it should capture at least 4 features.
	2. run pose_estimate mode node, obtain object_in_camera pose