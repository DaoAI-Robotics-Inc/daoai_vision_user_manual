Overview
==========================

Input
-------------------------------

* Cloud Ptr: a point cloud to be segmented
* Camera Intrinsic: camera intrinsic parameter used for RGBD segmentation
* RGB Pointer: RGB image to be segmented

Output
------------------------------

* preSegmRGB: rgb image before segmentation
* postSegmDepth: depth image of the scene after segmentation
* postSegmPCA: image showing PCA of the scene cluster 
* postSegmRGB: rgb image after segmentation
* results: a vector of segments, each containing a mask image of the size of the scene image, showing which points belong to this segment

Parameters
-----------------------

Pre-process
~~~~~~~~~~~~~~~~~~~~

* Basic Downsample: Level of downsampling when doing segmentation

Segmentation Parameters
~~~~~~~~~~~~~~~~~~~~~~~~~

* Basic Weight Threshold: how much different between the adjacent points to be considered as different segment. Default Value is 50, range is [0,100].
* Basic Min Size: minimum size of each segment. Default value is 50, range is [0,100].

Post-processing
~~~~~~~~~~~~~~~~~~~~~~~~

* Max Segment Size: Maximum size of the segment, segment greater than this will be removed. Default value is 100, range is [0,100].
* Min Segment Size: Minimum size of the segment, segment greater than this will be removed. Default value is 0, range is [0,100].
* Max Distance to Camera: Maximum distance of points in segment to camera, segment with points further than this distance will be removed. Off by default. Distance unit is millimeter
* Use Nan Removal: remove segment with more than 75% of the points invalid, if turned on.

