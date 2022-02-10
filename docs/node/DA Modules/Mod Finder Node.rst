Mod Finder Node 
==========

Synopsis 
---------
	Search edgel model on gray image. 


Reference Fixture 
---------
	Please refer to Reference Fixture System
	This node can be used for generating fixture. 


Model 
---------
	The model in this node is edgel model. Edge model use their edge-based geometric features (geometric features from extracted edges) to find the position of object.
	
	The model is defined by drawing a rectangle box on display. 
 .. image:: images/mod_finder_1.jpg
	:scale: 60%
|
	
	User may draw mask on the model to erase unwanted edges. After draw mask, run this node to apply changes
 .. image:: images/mod_finder_2.jpg
	:scale: 60%
 .. image:: images/mod_finder_3.jpg
	:scale: 60%
|

	The model can be searched on image. 
 .. image:: images/mod_finder_4.jpg
	:scale: 100%
|

Settings 
---------
	Image: <DataType: BPImage>
		for 2d mod_finder. The target image to search.
	da_depthmap_and_pointcloud: <DataType: SDaDepthNCloud>
		for 3d mod finder. The target depth map to search. This is an output of Da Depth N Cloud Conv Node. 
	timeout: 
		The time out for the node running.
	labelled mask sequence: <DataType: VecBPImage>
		An advance setting for input. By selecting a labelled mask sequence, the node will only search model matched mask region. The labelled mask sequence can be generated as output of DL segment node. Each mask must have same size as the image source. 
	Total Occurrences: 
		The occurrence for each model to search. If it is 1, then node will only search 1 object on image. If labelled_mask_sequence is enabled, then node will search 1 model on each matched mask region. 
	Speed: 
		Range [1, 4]
		
		The speed of searching. 
	Accuracy: 
		Range [1, 3]
		The accuracy of searching
	Smoothness: 
		Range [1, 100]
	
		Strength of the noise reduction filter. 
	Detail Level: 
		Range [1, 3]
		
		Sets the level of details to extract from model images and target images during edge extraction. The detail level determines what is considered an edge/background. A higher detail level will include more edges than a lower detail level.
	Shared Edge: 
		Range [0, 1]
	
		Sets whether to allow sharing of edges between occurrences.


Model Parameters 
---------
	Mask: 
		User can draw mask on model to remove unwanted edge. 
	Edit Pixel Map Size: 
		The size of pencil when drawing or erasing the mask.
	Label: 
		The label of model, only be used for matching labelled mask sequence. 
	Acceptance: 
		Range [0,100]
	
		Sets the acceptance level for the score. An occurrence will be returned only if the match score between the target and the model is greater than or equal to this level. 
	Certainty: 
		Range [0,100]
		
		Sets the certainty level for the score, as a percentage. If both the score and target scores are greater than or equal to their respective certainty levels, the occurrence is considered a match, without searching the rest of the target for better matches (provided the specified number of occurrences has been found). 
	Polarity: 
		Sets the expected polarity of occurrences, compared to that of the model. If the model is a white circle in black background, "SAME" will search for white circle in black background, "REVERSE" will search black circle in white background, and "ANY" will seach any circle in any background as long as the it is an edge. 
	Model Ref Point: 
		Set the center of the model, This point will be the output position of detected object. 
	Search Region: 
		The search region on target image. Can be used with fixture system. 


Output 
---------
	numFound: <DataType:Int>
		The totall number of occurrences found. 
	result: <DataType:ModFinderResult>
		A map, mapping "model_name" to "vector of occurrences of this model"
	success: <DataType:Bool>
		Boolean value indicating the search is successful
	modelPoses2D: <DataType:MapVecBPPose2D>
		A map of vector of 2d poses
	modelPoses3D: <DataType:MapVecBPPose3D>
		A map of vector of 3d poses
	modelMasks: <DataType:MapBPImage>
		A map of model masks
	labelledPose2dSequence: <DataType:VecBPPose2D>
		Vector of pose 2d preserving order from labelled mask sequence. 
	labelledPose3dSequence: <DataType:VecBPPose3D>
		Vector of pose 3d preserving order from labelled mask sequence. 
