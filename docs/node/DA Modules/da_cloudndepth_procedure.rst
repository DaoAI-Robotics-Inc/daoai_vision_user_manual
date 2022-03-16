Procedure of Using DA CloudNDepth Conv Node
===============================================

1. Link point cloud from camera node or reader node.
2. Change size of the depth image. Run the node.
3. Draw a bounding box to cover the points to be converted.
4. Now we have the depth image, 8 bit depth image output. The node's result can be used as input for Mod Finder node in 3d mode.
5. The depth to cloud mode takes in the output of cloud to depth mode. It can restore the point cloud from depth image.