Cloud To Depth Conversion Node
================================

This node converts a point cloud to a depth image, or a depth image back to point cloud.

.. image:: ../../_static/images/3d_process/cloud_depth_conversion.PNG
   :width: 100%

Input
-----------------

Input contains one of:

* Input Depth: depth image to be converted back to point cloud
* Input Cloud: point cloud to be converted to depth image


Output
--------------------

* cloud: restored point cloud from depth image
* depth: depth map from point cloud
* mask: A mask that shows which locations in depth image that has valid depth

Parameters
-----------------------

* Cloud to Depth
   * adjust bounding box: users can define area of interest by defining a bounding box using the adjust box interactor
   * Projection type: method used to convert point cloud to depth image, can be one of parallel pojection or pinhole Projection
   * FOV: field of view of Projection
   * Width: width of depth image
   * Height: height of depth image
* Depth to cloud
   * The depth image needs to be converted from point cloud using cloud to depth mode of this node. Otherwise, the node will use default camera intrinsics to construct point cloud from depth map


