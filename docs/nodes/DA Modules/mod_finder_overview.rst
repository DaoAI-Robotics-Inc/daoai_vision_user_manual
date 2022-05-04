Overview 
=====================

Reference Fixture 
---------------------
Please refer to Reference Fixture System. 

This node can be used for generating fixture. 


Model 
-----------------
The model in this node is edgel model. Edge model use their edge-based geometric features (geometric features from extracted edges) to find the position of object.
	
The model is defined by drawing a rectangle box on display. 
 .. image:: images/mod_finder_1.jpg
	:scale: 60%
	
You may draw mask on the model to erase unwanted edges. After draw mask, run this node to apply changes
 .. image:: images/mod_finder_2.jpg
	:scale: 60%
 .. image:: images/mod_finder_3.jpg
	:scale: 60%

The model can be searched on image. 
 .. image:: images/mod_finder_4.jpg
	:scale: 100%



Output 
--------------------
	
* numFound: (DataType:Int) The total number of occurrences found. 
* result: (DataType:ModFinderResult) A map, mapping "model_name" to "vector of occurrences of this model"
* success: (DataType:Bool) Boolean value indicating the search is successful
* modelPoses2D: (DataType:Map<Vec<Pose2D>>) A map of vector of 2d poses
* modelPoses3D: (DataType:Map<Vec<Pose3D>>) A map of vector of 3d poses
* modelMasks: (DataType:Map<Image>) A map of model masks
* labelledPose2dSequence: (DataType:Vec<Pose2D>) Vector of pose 2d preserving order from labelled mask sequence. 
* labelledPose3dSequence: (DataType:Vec<Pose3D>) Vector of pose 3d preserving order from labelled mask sequence. 
