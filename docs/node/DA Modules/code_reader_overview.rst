Overview
==========

	This node reads in an image, then detect the code on the image.
	The input will be considered as an gray image.
	The node can read 1d code or 2d codes base on node setting, such as:

	* code type
	* detect code amount
	* search region

	The output contains the information of the node, include:

	* the code string
	* the position of code

Use Case
---------
	When we want to read code on object to distinguish them. 

Node Settings 
----------------

	Image_In: (DataType:BPImage) The image with code on it. If the input is a color image, the node will consider it as a gray image.

	Num_to_Detect: the number of code to detect. Note Only 1D code types (excluding GS1 Databar, 4-state, Planet, and Postnet code types) and the 2D Data Matrix code type support searching for multiple occurrences.
	
	Code_Type: The type(format) of code to be detect


Advance Settings 
-----------------


	foreground_color: 
		Sets the foreground color of the code. 
	threshold_mode: 
		Sets the threshold mode used to internally binarize the source image
	threshold_value: 
		range [0, 255]
	
		Sets the threshold value used to internally binarize the source image, depending on the specified threshold mode. Note that if THRESHOLD_MODE is set to ADAPTIVE, this control type is ignored
	minimum_contrast: 
		range [1, 255]
		
		Sets the minimum possible contrast between the foreground and background in the target image for 1D codes (excluding Planet and Postnet) when using the ADAPTIVE threshold mode. Increasing the minimum contrast will typically improve code detection, particularly in the presence of noise and non-uniform lighting.However, if the minimum contrast is higher than the contrast of a code, the code will not be read correctly.For 2D codes, the minimum contrast is determined automatically, so the adaptive threshold mode does not use the minimum_contrast setting.
	speed: 
		Sets the search speed. The faster the search speed, the less robust the operation. For 1D code types, consider reducing the search speed when the pixel height of the bar code is small.For 2D code types, consider reducing the search speed when the cell size is small relative to the image size.
	time_out: 
		Specifies the maximum decoding time for an detection, in msec. default is 2000.
	error_correction: 
		Sets the type of error correction. This field will change base on different code type.
		
		Only 2D Aztec code type support percentage correction. 
		Range [5, 95]
	check_quiet_zone: 
		Sets whether the presence of the quiet zone is necessary for a successful detection of this code type. 
	string_format: 
		Sets the format of the output of the string.
	search_angle_value: 
		range [0, 360]
	
		Sets the nominal search angle. default is 0.
	search_angle_step: 
		range [0.1, 180.0]
	
		Sets the angle increment/decrement used when searching for a 1D code through an angular range.
	search_angle_delta_neg: 
		Sets the negative angular range of the search.
	search_angle_delta_pos: 
		Sets the positive angular range of the search.


Output 
---------
	result: (DataType: CodeReaderResult) The result of code reader, containing the information of the code.
		- decodedString: (DataType: Vector<String>) A vector of string, each contains the plaintext of a found code.

	numCodeDetect: (DataType: Int) The number of code detected
