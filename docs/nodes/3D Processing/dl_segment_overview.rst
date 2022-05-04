Overview
==============================

Input
-------------

* Cloud Ptr: point cloud used for segmentation
* Image Input: RGB image used for segmentation

Output
-------------
* bboxResults: a vector of bounding boxes of the segments. Each element contains top-left, bottom-right coordinate of each box.
* numDetected: number of segments detected.
* segmResults: a vector of segmentation results, for each segment.
   * center_pt: 2d point coordinate of the center.
   * centroid_3d: 3d point coordinate of the center.
   * depth: depth image.
   * eigen_vecs: eigen vectors representing trends of the variance.
   * label: label of the segment.
   * mask: mask of the segment, the mask has the size of the original image.
   * num_points: number of points in the segment.
   * pca: image representing PCA of the segment.
   * rgb: rgb image of the segment.
* success: whether segmentation is successful(finds at least one segment).

Deep Learning Parameters
-----------------------------

* Model Mode: use only RGB for classification; use only depth(from point cloud) for classification; or use both
* Model File Path: path to deep learning model
* Config File Path: path to deep learning config file
* Model Weights Path: path to model weights file
* Model Prediction Type: defines if the model is being used for segmentation of just the object (Detectron2 models) or if we are segmenting the picking positions (UNet).
* Model Sort Type: method to sort segmentation results, can be one of IOU Occluded, Binary Occluded, Area.
* Show Label: whether to display label of each segment.
* Post processing:
   * min/max area: values in the range [0,1] which represent the percentage of the image and segment can occupy.
   * min/max eigenval: Similar to how the segmentation calculates the PCA of each segment we calculate that here and limit the eigen values. Eigen value 1 is the longer axis.
   * min confidence: minimum confidence required for each segment.
   * NMS threshold: threshold for applying soft NMS to the bounding boxes. This removes boxes that are too close together. Default value is 0.8, range is [0,1].
   * Erosion/Dilation sizes: the kernel size used for erosion/dilation applied to segmentation mask and segmentation RGB image.
   * Erosion/Dilation iteration: number of times erosion/dilation is applied to segmentation mask and segmentation RGB image.
