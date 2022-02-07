Color Checker Node 
=========

Synopsis 
---------
	Do color matching or color segmentation on a color image.


Description 
---------
	Color Matching:
		match defined region with its nearest defined color
	Color Segmentation:
		Segment Image with defined color

Use Case
---------
	When we want to use color on similar objects to distinguish them. 

Node Settings 
---------
	Color Image In:  <DataType:BPImage>
		A color image. 
	Color Function: 
		decide weither user want to use Color_Matching function or Color Segmentation function.
	Tolerance: 
		Range [0 ~ 100]
		
		The global tolerance for color_samples. if you set this to 100, the tolerance will become infinite. default is 100.
	Confidence: 
		Range [0 ~ 100]

		Represents how confident you can be that the best-matched color-sample actually is the best possible match. 
		
		For example, a high confidence indicates that the best-matched color-sample must be vastly superior to all other color-samples, while a low confidence indicates that the best-matched color-sample only needs to be marginally superior to the other color-samples.


Advance Settings 
---------
	Color Space: 
		Specifies the conversion mode that the operation uses. 
	Match Distance: 
		Specifies the type of distance that the operation uses. Distance is the difference in color between the color-sample and the target area.
	Match Method: 
		Specifies the function used to match distance.
	Tolerance Mode: 
		Sets the strategy with which to use the tolerance value to calculate the acceptable (matching) color distance (tolerance) between the color-sample and a target area.
	Global Tolerance: 
		range [0.0, ~)
	
		Sets the acceptable tolerance for the color distance between the color-sample and a target area. The greater the tolerance, the greater the distance (difference) between the colors can be, for them to match. 
		
	Minimum Score: 
		range [0.0, 100.0]
	
		Sets the acceptance level for the color-sample's score. This score indicates the similarity between the color of the color-sample and the color of the target area. The higher the acceptance, the closer the colors must be for them to match.For a match, the color-sample must have a score that is greater than or equal to this level.
	Minimum Relative Score: 
		range [0.0, 100.0]
	
		Sets the acceptance level for the target area's relevance score. This score indicates the significance (relevance) of the match score. In statistics, this is similar to the confidence level; that is, it represents how confident you can be that the best-matched color-sample actually is the best possible match. 

		For example, a high relevance acceptance indicates that the best-matched color-sample must be vastly superior to all other color-samples, while a low relevance acceptance indicates that the best-matched color-sample only needs to be marginally superior to the other color-samples. 


Define Region 
---------
	In color segmentation, node will consider all defined region as a single combined region.
	In color matching, node will match each defined region to the nearest color sample.
	
	There is 3 way for defining a region:

	1. Use Image Mask. 
		user input a Image Mask that has same size as Color Image.
		Node will define only one single region base on the mask.
	2. Define from mod finder node
		user inputs a Mod Finder Result comes from mod_finder node
		user select one model in Mod Finder Result.
		One region will be defined for each object found from mod_finder.
		User can draw mask on model to define the color match region related to object
	3. Define from display
		User draw a rectangle box from main display
		User can draw mask for this region


Color Sample 
---------
	The node will only match regions to defined color
	
	There are 2 ways to define a color sample

	1. Define color by area.
		User draw a box on display, node will calculate the average color of this box, and save it as color sample value.
	2. Define color by value
		User will define a RGB value as color sample


Output 
---------
	result: <DataType: ColorCheckerResult>
		Color Checker Output