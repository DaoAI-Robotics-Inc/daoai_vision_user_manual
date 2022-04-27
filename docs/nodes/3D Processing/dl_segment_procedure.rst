Procedure of Using DL Segmentation Node
===========================================

DL segmentation can be performed on one of point cloud, image, or both.
Note that DL segmentation works best when the input contains background information around the object. In pre-processing,
avoid using filters like color filter that may remove the background and only keep the object.

Steps in using DL segmentation node

1. Pre-process the scene with ROI or adjust bounding box operation. This will improve search efficiency
2. Run DL segmentation to find object segments from the scene
3. (Optional) Post-process the segment masks

After segmentation, you can use the result in following ways.

1. Use center point of the segments as the 2D positions of object. Estimate 3d positions using reconstruct node. Use these 2D poses or 3D poses to determin picking positions
2. Use scene crop to devide a scene point cloud into a vector of point clouds, each contains point cloud of one object
3. More.

Adjusting Segment Mask Size With Post-processing
----------------------------------------------------

The intial result of the DL segmentation node may not contain all the points of the object because many deep learning model use dowmsampling for prediction.
You can adjust the size of the segment based on your need (to reduce possible noise or to include as much object information as possible) using erosion
and dilation post-processing option.

Below image shows the result of erotion, the result mask is smaller than the actual object

.. image:: Images/dl_segment/erosion.png
   :width: 100%