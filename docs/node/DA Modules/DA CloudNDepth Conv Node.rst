Da Depth N Cloud Conv Node 
=========

Overview
---------
Synopsis 
~~~~~~~~~
	Generate Calibrated Depth Map Image from Point Cloud.

	Generate Point Cloud from Calibrated Depth Map.

Use Case:
	When we need a calibrated depth image from point cloud to do 3d searching in node such as 3d mod_finder, metrology node, measurement node.  

Input
~~~~~~~~~
	Depth Map <DataType: BPDepthImage>
		For Depth to Cloud, the depth map.
	PointCloud
		For Cloud to Depth, the point cloud
	Depthmap Size X,Y
		For Cloud to Depth, set the size of depth image.
	Extraction Box Settings
		For Cloud to Depth, set the extraction box.
		Only points inside the box will be extracted into depth map.
		Normally these parameters are tunned by adjust box on interactive display when running the node.

Description 
~~~~~~~~~
	Depth Map -> Point Cloud:
		For each pixel point in depth image, generate a point with its depth value and add it into pointl cloud.
	
	Point Cloud -> Depth Map:
		User set the size_x and size_y of depth image. From point cloud, draw a box in point cloud.
		For all the points in the box, select the top points and put it as pixel points of depth image. 
		Then remap the depth image to a size_x,size_y depth image.  


Output 
~~~~~~~~~
	Depth Map -> Point Cloud:

	* Generated Point Cloud <DataType: BPPointCloud>
		Output of Depth to Cloud
	* Generated Depth Map <DataType: BPDepthImage>
		Output of Cloud to Depth.
	* Generated 8bit Depth Map <DataType: DepthImage>
		Output of Cloud to Depth.

