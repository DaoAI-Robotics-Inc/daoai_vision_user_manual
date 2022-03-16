Overview 
==============

This node allows you to find markers (for example, edges) in an image, based on differences in pixel intensities. Upon finding a marker, the node outputs the marker's spatial reference position and measures features such as its width and angle. You can calculate measurements between two markers, such as the equation of the line that joins them.  


Reference Fixture 
---------------------

	Please refer to Reference Fixture System


Interactive Display 
-------------------------

	user may only be able to edit or add markers after click "Show Interactive Display"


Markers 
--------------------

	User may click "+" button to add a new marker.

	Edge Marker: 
		draw a rectangle region, and detect edges in this region
		the detection is base on pixel value derivative
		the detection direction is the arrow direction shown on region
	
	Circle Marker: 
		draw a circle region, detect circle inside the region
		the detection is base on detecting edges from center to 8 outer directions
		the detection direction is from center to outer
	
	Stripe Marker: 
		draw a rectangle region, detect stripes(pair of edges) in the region
		the detection direction is the arrow direction shown on region

Output 
-------------------

	result: the measurement result, containing the information of markers such as its position, size, and radius for circle.