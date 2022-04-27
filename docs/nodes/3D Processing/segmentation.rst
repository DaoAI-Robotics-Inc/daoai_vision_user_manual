Segmentation Node
================================

.. image:: Images/segmentation.png
   :width: 100%


The Segmentation Node clusters the points from an input point cloud into segments. The output segment masks can be used by the Scene Crop Node to create a vector of segment clouds. 
The matching process will run faster on these segments.

RGBD segmentation works best when instances of objects are spaced apart. 
Otherwise, segments may contain multiple instances of the object. In these cases, normal segmentation may segment out the instances more clearly. 
Both watershed segmentations are performing on the image using maker generation. They are faster but could result in less accurate segmentation.

Four types of Segmentation Nodes are available:
   * Segmentation RGBD: Uses the RGB and depth information to perform clustering
   * Segmentation Normal: Uses the normals in the point cloud to perform clustering
   * RGB only: Performs segmentation on an RGB image.
   * Depth only: Performs segmentation on a Depth image. 

.. toctree::
   :maxdepth: 1

   segmentation_overview
   segmentation_procedure