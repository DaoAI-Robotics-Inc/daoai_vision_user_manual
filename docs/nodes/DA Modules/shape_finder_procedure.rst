Procedure of Using Shape Finder Node
======================================

1. Link input image
2. Run the node, to load the image
3. Open "show ruler" in the display option
4. Define shape. the unit of parameters are the unit of ruler showed on display.
5. Run the node, will output the poses and mask of founded shape


Parameter Tunning 
----------------------

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