Procedure in Using DL Classification Node
===============================================

DL classification can be performed on any point cloud or image. However in most cases there will be multiple objects in the scene with 
different classes, so it is better to separate out each objects. This can be completed using DL segmentation node.

The steps to use DL classification node:

1. Separate out each objects in point cloud or image. The purpose of this step is to obtain point clouds or image, each containing an object to classify 
2. For each object in 1. Use DL classification to determine the type of the object
3. Based on object label output, do different actions

.. image:: ../../_static/images/3d_process/dl_classify/sample_flowchart.png
   :width: 100%


