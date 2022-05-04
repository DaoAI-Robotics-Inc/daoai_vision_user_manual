Procedure of Using Segmentation Node
=========================================

To get the best segmentation result, is it recommended to use DL segmentation node with pre-trained model.
However, it is possible to produce the desired segmentation using segmentation node.

Steps in using DL segmentation node

1. Pre-process the scene with ROI or adjust bounding box operation. This will improve search efficiency
2. Run DL segmentation to find object segments from the scene
3. (Optional) Post-process the segment masks

After segmentation, you can use the result in following ways.

1. Use center point of the segments as the 2D positions of object. Estimate 3d positions using reconstruct node. Use these 2D poses or 3D poses to determine picking positions
2. Use scene crop to divide a scene point cloud into a vector of point clouds, each contains point cloud of one object
3. More.

Tunning Segmentation Parameters for Better result
-----------------------------------------------------

You can adjust segmentation parameters for better result. To reduce the background effect, increase the *Basic Weight Threshold*.
Changing *Basic Min Size* to get the desired segment size.

You can also change segment size by changing *Max Segment Size* and *Min Segment Size* in post-processing.