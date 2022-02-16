Shape Finder Node 
=========

Overview
---------
Synopsis 
~~~~~~~~~
	Search shape on gray image. 
	
 .. image:: images/shape_finder_3.jpg
	:scale: 90%
	:align: center
|

Reference Fixture 
~~~~~~~~~
	Please refer to Reference Fixture System
	This node can be used for generating fixture. 


Shape 
~~~~~~~~~
	User can define shape and shape parameters.
	The parameters for different shape is labelled on the shape model.
	Please note that the unit of parameters are pixel unit. 
 .. image:: images/shape_finder_2.jpg
	:scale: 90%
	:align: center
|	
	
	On the screen, the pixel units are labelled if you click "Show Ruler" in display setting.
 .. image:: images/shape_finder_1.jpg
	:scale: 100%
	:align: center
|

	The result of shape search is as below
 .. image:: images/shape_finder_3.jpg
	:scale: 90%
	:align: center
|


Output 
~~~~~~~~~
	numFound: <DataType:Int>
		The total number of occurrences found. 
	shapeLocations: <DataType:VecBPPose2D>
		Shape 2D poses map. 
	shapeMasks: <DataType:VecBPImage>
		Shape masks map. 
	success: <DataType:Bool>
		If all shape search are performed successfully. 
		
		
Procedure of Using This Node
---------
1. inptu image
2. run the node, to load the image
3. open "show ruler" in the display option
4. define shape. the unit of parameters are the unit of ruler showed on display.
5. run the node, will output the poses and mask of founded shape


Parameter Tunning 
---------

Settings 
~~~~~~~~~
	timeout: 
		The time out for the node running. Unit is msec. 
	Speed: 
		The speed of searching. 
	Accuracy: 
		The accuracy of searching
	Create Solid Mask: 
		If not clicked, the shape mask will only include the shape edge. But if the solid mask option is clicked, the mask will include include the edge and inside it.

Shape Settings 
~~~~~~~~~
	Shape: 
		The shape to search. 
	Foreground Color:
		The foreground color of shape. For most shape, it is ANY. For Circle shape, it is Black.
		Circle shape do not support Foreground Color "ANY".
	Param2-6:
		The param of shape, such as radius of circle. The unit is pixel, as shown on "show ruler" option. 
	Min Acceptance: 
		Sets the acceptance level for the score. An occurrence will be returned only if the match score between the target and the model is greater than or equal to this level.
	Total Occurrences:
		The number of occurrences to search. 
	Search Region:
		the search region of shape, can be used with fixture system. 