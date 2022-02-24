Overview
========================

Input
------------------

* Model Mesh: a point cloud or polygon mesh, representing the model
* Scene Cloud: scene point cloud
* Hypothesis: a vector of poses for each occurrence of model in scene

Output
------------------

* poses: a vector valid poses after verification, will be sorted if stacking mode is used

Parameters 
--------------------

* Confidence: the confidence of a pose to be valid. Default is 50, range is [0,100]
* Depth Mode Parameters
   * Occluded Part Tolerance: threshold such that poses with more than this part occluded should be removed. Default is 50, range is [0,100]
   * Error Tolerance: how much error points a pose can have. Higher the tolerance, more inaccurate result will be kept. Default is 50, range is [0,100]
   * Overlap Ratio: controls the pentalty low overlap between model and scene. Default is 50, range is [0,100]
* Edge Mode Parameters
   * Camera Instrinsic Parameter: camera intrinsic parameter, used for edge extract
   * RGB image: RGB image of the scene
   * Smoothness: level of smoothness applied to scene edge. Default is 50, range is [0,100]
   * Canny Low Factor: lower threshold of canny filter
   * Canny High Factor: upper threshold of canny filter
   * Angle Threshold: angle threshold for smoothing the extracted edges
   * Contrast threshold: threshold for filtering out edges with low difference in depth
   * Search Radius: radius used for edge pixel clustering
* Stacking Mode Parameters
   * FOV: field of view for viewing camera, greater value means more poses will be seen, and then kept.

