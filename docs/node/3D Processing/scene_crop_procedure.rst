Procedure of Using Scene Crop Node
==========================================

1. Use segmentation node or DL segmentation node to obtain a vector of masks
2. Use scene crop node to crop the scene point cloud into a vector of sub-point clouds, based on the segmentation masks obtained in previous segmentPoses
3. Use a loop sub-flowchart to iterate through each point cloud to process them separately, or feed the whole vector of point clouds into nodes like box volume estimation node to process them as a whole

