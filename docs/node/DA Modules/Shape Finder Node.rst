Shape Finder Node 
=========

Synopsis 
---------
	Search shape on gray image. 


Reference Fixture 
---------
	Please refer to Reference Fixture System
	This node can be used for generating fixture. 


Shape 
---------
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

Settings 
---------
	Image: <DataType:BPImage>
		The target image to search.
	timeout: 
		The time out for the node running. Unit is msec. 
	Speed: 
		The speed of searching. 
	Accuracy: 
		The accuracy of searching
	Create Solid Mask: 
		If not clicked, the shape mask will only include the shape edge. But if the solid mask option is clicked, the mask will include include the edge and inside it.


Output 
---------
	numFound: <DataType:Int>
		The total number of occurrences found. 
	shapeLocations: <DataType:VecBPPose2D>
		Shape 2D poses map. 
	shapeMasks: <DataType:VecBPImage>
		Shape masks map. 
	success: <DataType:Bool>
		If all shape search are performed successfully. 
