Mod Finder Node 
================

Overview 
--------------------
	The DaoAI Mod Finder engine used images pattern feature to find the object in 2D space, then used 3D space conversion to map it to 3D space. Usually at the end, it will go through point cloud alignment node to improve the 3D position accuracy.
	
	The Mod Finder can be configured to find 2D or 3D model.

Input and Output 
--------------------
	
+----------------------------------------+-------------------------------+-------------------------------------------------------------------------------+
| Input                                  | Type                          | Description                                                                   |
+========================================+===============================+===============================================================================+
| Image (2D Mod Finder)                  | Map<Image>                    | The source that is used to search for model.                                  |
+----------------------------------------+-------------------------------+-------------------------------------------------------------------------------+
| or                                     |                               |                                                                               |
+----------------------------------------+-------------------------------+-------------------------------------------------------------------------------+
| DA_Depth_Cloud_result (3D Mod Finder)  | Da_Depth_N_Cloud_Conv_Result  | - The source that is used to search for model.                                |
|                                        |                               | - The DA_Depth_Cloud_result is the output of the "DA CloudNDepth Conv" node.  |
|                                        |                               | - It is the combination of a Da Depth Map and a Point Cloud.                  |
+----------------------------------------+-------------------------------+-------------------------------------------------------------------------------+


+-------------------------+-------------------+------------------------------------------------------------------------+
| Output                  | Type              | Description                                                            |
+=========================+===================+========================================================================+
| labelledPose2dSequence  | Vec<Pose2D>       | Vector of pose 2d preserving order from labelled mask sequence.        |
+-------------------------+-------------------+------------------------------------------------------------------------+
| labelledPose3dSequence  | Vec<Pose3D>       | Vector of pose 3d preserving order from labelled mask sequence.        |
+-------------------------+-------------------+------------------------------------------------------------------------+
| modelMasks              | Map<Image>        | A map of model masks.                                                  |
+-------------------------+-------------------+------------------------------------------------------------------------+
| modelPoses2D            | Map<Vec<Pose2D>>  | A map of vector of 2d poses.                                           |
+-------------------------+-------------------+------------------------------------------------------------------------+
| modelPoses3D            | Map<Vec<Pose3D>>  | A map of vector of 3d poses.                                           |
+-------------------------+-------------------+------------------------------------------------------------------------+
| numFound                | Int               | The total number of occurrences found.                                 |
+-------------------------+-------------------+------------------------------------------------------------------------+
| result                  | ModFinderResult   | A map, mapping “model_name” to “vector of occurrences of this model”.  |
+-------------------------+-------------------+------------------------------------------------------------------------+
| success                 | Bool              | Boolean value indicating the search is successful.                     |
+-------------------------+-------------------+------------------------------------------------------------------------+

Node Settings
---------------
	The following screen shots demonstrate the settings of the 2D mod finder.

	The only difference between the settings of 2D mod finder and the 3D mod finder is the "Image" input in the "Source" section for 2D is replaced by "Da Depth Map And Point Cloud" for 3D.

Source Parameters
~~~~~~~~~~~~~~~~~

.. image:: images/mod_finder_settings_1.png
	:scale: 100%

- **Image**: 

	The source that is used to search for model. Using link expression to link the image.


- **Time Out**: (Default value: 2000 ms) 

	The time limit for the node to run. When the running time of the node reaches the time limit. The node will terminate and return the current output. 


- **Use labelled mask sequence**: TO DO


Algorithm Parameters
~~~~~~~~~~~~~~~~~~~~

.. image:: images/mod_finder_settings_2.png
	:scale: 100%


- **Total Occurrences**: Range [0,∞) (Default value: ONE)

	The number of occurrences for each model to search. 
	The occurrence can be set to any positive number. 
	If the number of detected object is larger than the total occurrences number, 
	the objects with the highest acceptance will be returned. 
	If the occurrences number is larger than the number of detected objects, 
	all of them will show. The Total Occurrences can be set to "ALL". 

	(left: occurrences = 1, middle: occurrences = 2, right: occurrences = ALL)

	.. image:: images/mod_finder_5.jpg
		:scale: 60%
	.. image:: images/mod_finder_6.jpg
		:scale: 60%
	.. image:: images/mod_finder_7.jpg
		:scale: 60%

- **Speed**: Range [1,4] (Default value: MEDIUM)

	The speed of searching. Larger value means faster speed but less accuracy.


- **Accuracy**: Range [1,3]  (Default value: DISABLE)

	The accuracy of searching. Larger value means higher accuracy but slower speed.
	

Edge Selection Parameters
~~~~~~~~~~~~~~~~~~~~~~~~~


.. image:: images/mod_finder_settings_3.png
	:scale: 100%


- **Smoothness**: Range [0,100) (Default value: 50)

	The noise reduction used during edge extraction. Larger value means stronger noise reduction.
	A high smoothness will only accept smooth edges, and low smoothness will accept sharp edgeds. 
	
	(left: smoothness = 100, right: smoothness = 1)

	.. image:: images/mod_finder_8.jpg
		:scale: 60%

	.. image:: images/mod_finder_9.jpg
		:scale: 60%

- **Detail Level**: Range [1,3] (Default value: MEDIUM)

	The level of detail during edge extraction. The detail level determines what is considered as an edge/background. Larger value means more edges are extracted.


- **Shared Edge**: Range [0,1]  (Default value: DISABLE)

	Whether edges are shared bewteen different occurrences.


Models
~~~~~~
	The model is defined from the scene, or it can be imported from a DL_Segment node using labelled mask sequence.
	For the details of the defining or import process, please check the "Procedure to use" section. 
	This section focusses on the properties of models.

	.. image:: images/mod_finder_settings_4.png
		:scale: 60%

- **Label**: (Default value: -1)

	asd

- **Acceptance**: Range [0,100] (Default value: MEDIUM)

	The minimum matching score where an occurrence is accpeted. 
	An occurrence will be returned only if the match score between the target and the model is greater than or equal to this level.


- **Certainty**: Range [0,100] (Default value: HIGH)

	Sets the certainty level for the score, as a percentage. 
	If both the score and target scores are greater than or equal to their respective certainty levels, 
	the occurrence is considered a match, without searching the rest of the target for better matches 
	(provided the specified number of occurrences has been found).


- **Polarity**: 

	the expected polarity of occurrences, compared to that of the model. 
	If the model is a white circle in black background, 
	“SAME” will search for white circle in black background, “REVERSE” will search black circle in white background, 
	and “ANY” will search any circle in any background as long as the it is an edge.


	.. image:: images/mod_finder_11.jpg
	:scale: 100%

Model Masking
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




Procedure of Using Mod Finder Node
-----------------------------------

	1. Link input model image. For 3d mod finder node, the input must be the output of DA CloudNDepthConv Node.
	2. Run node once so the input image shows on the display.
	3. Define model, click on "+" button to add a model, and draw a bounding box in the input image to define the model.
	4. (Optional) adjust model in the model config page.
	5. Run the node with other images. The found occurrences of the model will be displayed in the target image.
	6. Use the position vector  for further processing to get the picking pose of the objects in the scene.

Model Configuration
-------------------------

	You can adjust the detail of the model in the model config page. Double click or select model and click edit button to open model config page.

	.. image:: images/mod_finder_config.png
		:scale: 60%

	The red lines are the extracted edges of the model, which will be used for searching. You can mask out or unmask area that you are not interested in by clicking "Draw Mask" or "Erase Mask" button.
	This will enter interactor mode where you can edit mask. You can also change "Edit Pixel Map Size" to change the brush size when drawing and erasing mask.

	You can also define reference point in the model image by clicking "Define Ref Point" of the model. This will enter interactor mode where you need to select a point as a reference point.
	Normally the reference point is the center of all the edge pixels. It is recommended to use the default reference point.

	Additionally, you can define the search region in the target image by clicking "Define Search Region" and draw a rectangle ROI on target image.

Search Model In Labelled Mask Sequence 
--------------------------------------

	This is a special use case of mod finder where the input is the result of segmentation (a vector of image, each contains an object) instead of a single image.

	1. Use DL segmentation node to obtain segments and their labels.
	2. In mod finder node, define models. Assign correct labels to the models.
	3. Check "Use Labelled Mask Sequence", and link the labelled mask sequence to mask sequence output of of the DL segmentation node.
	4. Run the node. For each mask image in the sequence the node will search for the model based on the model of the mask image (label of the segment).
	5. The result pose (sorted in labelledPose2dSequence or labelledPose3dSequence) will have the same order of the segments vector of the DL segmentation node.

Parameter Tunning 
------------------

Settings 
--------------------

	The occurrence for each model to search. If it is 1, then node will only search 1 object on image. If labelled_mask_sequence is enabled, then node will search 1 model on each matched mask region. 

	.. image:: images/mod_finder_5.jpg
		:scale: 60%
	.. image:: images/mod_finder_6.jpg
		:scale: 60%
	.. image:: images/mod_finder_7.jpg
		:scale: 60%

	Speed: 

		Range [1, 4]	
		
		The speed of searching. 

	Accuracy: 

		Range [1, 3]
		
		The accuracy of searching

	Smoothness: 

		Range [1, 100]
	
		A high smoothness will only accept smooth edges, and low smoothness will accept sharp edgeds. 
		Below the first image is when smoothness=100, and the second one is when smoothness=1.


	.. image:: images/mod_finder_8.jpg
		:scale: 60%

	.. image:: images/mod_finder_9.jpg
		:scale: 60%

			
	Detail Level: 

		Range [1, 3]
			
		Sets the level of details to extract from model images and target images during edge extraction. The detail level determines what is considered an edge/background. A higher detail level will include more edges than a lower detail level.
			
	.. image:: images/mod_finder_9.jpg
		:scale: 60%
	.. image:: images/mod_finder_10.jpg
		:scale: 60%


	Shared Edge: 
		
		Range [0, 1]
		
		Sets whether to allow sharing of edges between occurrences.


Model Parameters 
------------------

	Acceptance: 

		Range [0,100]
		
		Sets the acceptance level for the score. An occurrence will be returned only if the match score between the target and the model is greater than or equal to this level. 

	Certainty: 
		
		Range [0,100]
		
		Sets the certainty level for the score, as a percentage. If both the score and target scores are greater than or equal to their respective certainty levels, the occurrence is considered a match, without searching the rest of the target for better matches (provided the specified number of occurrences has been found). 

	Polarity: 

		Sets the expected polarity of occurrences, compared to that of the model. If the model is a white circle in black background, "SAME" will search for white circle in black background, "REVERSE" will search black circle in white background, and "ANY" will search any circle in any background as long as the it is an edge. 

	.. image:: images/mod_finder_11.jpg
		:scale: 100%	


Reference Fixture 
---------------------
	Please refer to Reference Fixture System. 

	This node can be used for generating fixture.