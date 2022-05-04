Marker Parameter Tunning 
===========================
	Number of Occurrences: 
		The number of maximum edge to detect, default is 1.
 .. image:: images/measurement_1.JPG
	:scale: 60%
 .. image:: images/measurement_2.JPG
	:scale: 60%
|

	Min Occurrences: 
		Minimum number of edge to detect. if detected less edge, then it is a detection fail. 
	Polarity: 
		The polarity of edge to detection direction. Positive is from black to white, Negative is from white to black.

 .. image:: images/measurement_3.JPG
	:scale: 60%
 .. image:: images/measurement_4.JPG
	:scale: 60%
|

	Polarity2: 
		For stripe markers, decide the polarity of the second edge of stripe, related to stripe's first edge.

 .. image:: images/measurement_5.JPG
	:scale: 60%
 .. image:: images/measurement_6.JPG
	:scale: 60%
|

	Max Association Distance: 
		not range limit, unit is pixel. 
	
		The maximum distance between a marker's edge (either straight or circular) and its associated sub-edges during fit operation. 

		For edge and stripe markers, it is measured perpendicular from the fitted edge position, along to the search direction.

		For circle markers, it is measured radially from the fitted circle perimeter
	Min Edge Value: 
		Range [0, 100]
	
		The confidence of edge detection. A high value will ignore edges with weak contrast. Default is 2.0. 
 .. image:: images/measurement_7.JPG
	:scale: 60%
 .. image:: images/measurement_8.JPG
	:scale: 60%
|