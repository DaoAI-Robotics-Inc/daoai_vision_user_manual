Metrology Node
=========


Overview
---------
Synopsis 
~~~~~~~~~
	Define, Detect or Calculate features such as edge, circle, and point on a gray image.
	Calculate value information such as length of segment and radius of circle and arc. 
 .. image:: images/metrology_0.jpg
	:scale: 60%
 .. image:: images/metrology_1.jpg
	:scale: 60%
|

Reference Fixture 
~~~~~~~~~
	Please refer to Reference Fixture System


Interactive Display 
~~~~~~~~~
	User may only be able to edit or add features after click "Show Interactive Display"

Output 
~~~~~~~~~
	allTolerancesPassed: <DataType:Bool>
		a boolean value indicating if all tolerances are passed
	numPassedTolerances: <DataType:Int>
		number of passed tolerance
	numWarningTolerances: <DataType:Int>
		number of warning tolerance
	numFailedTolerances: <DataType:Int>
		number of fail tolerance
	toleranceResult/tolerance_name['']: <DataType:Double>
		the actual value of the tolerance


Procedure of Using This Node
---------
1. input Image.
2. open interactive display
3. define Features
4. define Tolerances
5. run the node, the node will output the tolerance values and tolerance pass/fail

Feature and Tolerance
---------
Features 
~~~~~~~~~
	There are 3 ways for defining a feature:
	Parametric Feature: 
		define fixture in absolute position.
	Measured Feature:
		define a region in absolute position, detect edge features such as segment and circle in the region.
	Constructed Feature: 
		define fixture from other features, such as define a mid_point from a segment, or define a circle base on 2 points.

	After a feature is defined, the feature(or region for measurement features) will appear in the interactive display at position (0,0)
	user can drag it to proper position. 
	
	For measured features, the detection direction is shown as arrow on the edge of searching region.
	Below is an example of having 2 measured circle. the blue ring is search region, and the red circle is detected.
 .. image:: images/metrology_feature_example.jpg
	:scale: 60%
|


Measured Feature Parameters 
~~~~~~~~~
	Threshold: 
		A high threshold only keeps edge with strong contrast. A low threshold will include fainter edges.
	Smoothness: 
		Range [0.0 ~ 100.0]
	
		Strength of the noise reduction filter when detecting edges. 
	Data Angle Tolerance: 
		Whether edges along a transition are considered is based on the angle(direction) of the transition compared to the scan direction of the search region. This angle tolerance determines the range of accepted angle(direction). 
	Edge Selection Rank: 
		Setting rank "1" will fit the segment to the edges closest to the beginning of the search box. Setting "Disable" will fit to all the edges found in the search-box. 


Tolerance 
~~~~~~~~~
	Tolerance is a calculation of features. such as the maximum distance between 2 features.
	user can add tolerance, and set the pass_min, pass_max, warn_min, warn_max for it.
	normally, it is:
		warning_min < pass_min < pass_max < warning_max

	If the value is between pass_min and pass_max, then it is a pass tolerance,
	else if the value is between warning_min and warning_max, then it is a warning tolerance,
	else if the value is outside of warning_min or warning_max, then it is a fail tolerance.

	Below is an example of measuring the minimum distance of 2 circle feature:
 .. image:: images/metrology_tolerance_example.jpg
	:scale: 60%
|
