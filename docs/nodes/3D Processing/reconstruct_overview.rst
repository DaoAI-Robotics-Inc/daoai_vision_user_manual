Overview
=======================

Input
----------------------------

* Point Cloud: The captured point cloud of the target scene.
* Object Locations: The result from 2D mod_finder/ shape_finder/ dl_segm.
* Camera Intrinsic 
* Object masks: The masks of the detected model (2D mod_finder) or detected shapes (shape_finder). Not necessary when not using the mask for Z and Rotation computation. 
  
Output 
-------------------------------

* objectPositions: 3d poses computed from the 2d poses

Estimating Z value
--------------------------------

The node has two ways of constructing z value in 3d poses
* Averaging Surrounding Points: This is the default method which uses a set of surrounding points  (square kernel) around the reference point and converts them to a point cloud (using the input point cloud) and takes the average Z value of the corresponding 3D points in the point cloud. The size (radius) of the kernel can also be defined by the user. Using a bigger kernel will result in using more surrounding points for Z computation.  
* Averaging masking area: This method uses the mask obtained from mod-finder , shape-finder or dl_segm to obtain the Z value by using the non-zero pixels in the mask (model mask, shape mask or segment mask  depending on which node you are using  before reconstruct_node) and taking the average Z value of their corresponding points in the point cloud. There is also a dilation iterations parameter that can be used to dilate the model/shape mask if needed. More dilation results in using more points for Z computation. 

Enable Rotation computation
--------------------------------

If this option is checked by the user, the program will compute the rotation of the object with respect to the camera coordinates system. 
The nodes has two ways of constructing rotation
* Surrounding Normal Points: This is the default method which uses a set of surrounding points of the reference point to fit a plane in the point cloud and then, uses this plane to find normal vector which is then used for rotation calculation. However, this method can fail if the surrounding points are nan (invalid), especially in cases that the target shape/ model is a hole. However, you have control in the kernel used around the reference point to fit the plane and calculate the rotation. 
* Mask Region Normal: This method uses the mask obtained from mod-finder, shape-finder or dl_segm and converts it to a cloud to obtain the Rotation value by using the non-zero pixels in the mask and fitting a plane to the corresponding 3D points. Then, the normal of the plane estimated which is used for rotation calculation. There is also a dilation iterations that can be used to dilate the model/shape/segment mask if needed. More dilation results in using more points for plane fitting and Rotation calculation. This option is especially good for cases that we have detected a shape/model which is actually a hole. In this scenario, most of the cases, the reference point and the surrounding points are nan. Therefore, using the surrounding points is not able to find the normal (unless a big kernel size is used) but using the mask region will use the mask to fit the plane and ignore the nan points. 

