Basic Node Inputs and Outputs
===========
Int:
	An integer value (no decimal places)
Double:
	A numerical values which can have decimal places.
Bool:
	A boolean value which can be either True (1) or False (0).
String:
	Can be any combination of characters (e.g. "xyz123!").
Image:
	A 2D array of information, often RGB or just greyscale, represented by pixels.
Depth Image:
	A 2D array of information which also inludes a parameter that represents distance from the data acquisition device (i.e. a 3D camera).
Point Cloud:
	A set of data points that represent an object in 3D, where each point has at least an X, Y, and Z component, and which may often also have colour components. Unlike a depth image, a point cloud is not organized into a grid-like array where each array element has data - a point cloud can have no points in part of the cloud and lots of points in other parts. Point clouds can be read in using the Camera Node or Reader Node using .pcd, .daf or .dcf files or by connecting to a camera. 
Mesh: 
	Similar to a Point Cloud as a set of 3D data points are also stored, but a Mesh also includes another set of information that represents a surface defined by points which form polygons that make up the surface. Can be read in using the Reader Node using .ply, .stl, or .obj files.
Camera Intrinsics:
	Holds information about the physical camera in use, such as focal length. Can be obtained by reading a .dcf file or connecting to a camera with the Camera Node. 
Pose:
	A numerical description of the position and orientation of an object. Position is given in X, Y, and Z coordinates and orientation can be given in different ways including quaternion or angle-axis representation. Can be generated using the Assemble Pose node.

