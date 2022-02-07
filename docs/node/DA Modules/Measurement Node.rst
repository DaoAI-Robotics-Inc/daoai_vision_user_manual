Measurement Node 
=========

Synopsis 
---------
	Find and measure edge, circle, stripe on a gray image.


Description 
---------
	This node allows you to find markers (for example, edges) in an image, based on differences in pixel intensities. Upon finding a marker, the node outputs the marker's spatial reference position and measures features such as its width and angle. You can calculate measurements between two markers, such as the equation of the line that joins them.  


Reference Fixture 
---------
	Please refer to Reference Fixture System


Interactive Display 
---------
	user may only be able to edit or add markers after click "Show Interactive Display"


Markers 
---------
	User may click 【+】 button to add a new marker.

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


Marker Parameters 
---------
	Number of Occurrences: 
		The number of maximum edge to detect, default is 1.
	Min Occurrences: 
		Minimum number of edge to detect. if detected less edge, then it is a detection fail. 
	Polarity: 
		The polarity of edge to detection direction. Positive is from black to white, Negative is from white to black. 
	Polarity2: 
		For stripe markers, decide the polarity of the second edge of stripe, related to stripe's first edge.
	Max Association Distance: 
		not range limit, unit is pixel. 
	
		The maximum distance between a marker's edge (either straight or circular) and its associated sub-edges during fit operation. 

		For edge and stripe markers, it is measured perpendicular from the fitted edge position, along to the search direction.

		For circle markers, it is measured radially from the fitted circle perimeter
	Min Edge Value: 
		Range [0, 100]
	
		The confidence of edge detection. A high value will ignore edges with weak contrast. Defaule is 2.0. 


Output 
---------
	result: 
		the measurement result, containing the information of markers such as its position, size, and radius for circle.

