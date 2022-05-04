Overview
=====================

Input
---------------------
* Box segments: a vector of point cloud, usually from segmentation node or DL segmentation node, each contains that point cloud of a box object
* Origin: a pose representing the position of reference coordinates, all boxes will have its top surface on the x-y plane of the reference coordinates
* Scene cloud: a point cloud that contain the original scene, used for visualization

Output
------------------------
* boxPoses: a vector of poses, representing the picking pose of each box
* dimensions: a vector of triples, representing the picking 

Node Parameters
---------------------------
* Use OBB: Choose the kind of bounding box. If unselected, box will be oriented in line with the computer axes. If selected, bounding box will be perpendicular to the cloud's eigenvectors, which are shown visually through the pose direction. In both cases, the reference frame is accounted for.
   * Use 2d Correction: whether to use 2d information to correct rotation around z axis for the box position and picking pose

* Choose Centroid Pose: If selected, the pose's position for each box will be based on the weighted center of the point cloud, as opposed to the center of the box. 
* Correct Pose Rotation: Selecting this will rotate each pose such that the amount of rotation from the identity pose doesn't deviate past pi/2. In other words, the red arrow of each pose always has a positive x-component.
* Downsample Strength: Downsamples each cloud by creating a voxel grid and averaging all points in each voxel into a single point. In basic operation, this is a value from 0-100. In advanced operation, you can specify the dimensions of the voxels. Higher downsampling leads to faster operation, at the potential cost of worse results.
* Lock Z axis: if selected, the z axis of every picking pose will have the same direction as the z axis of reference pose.