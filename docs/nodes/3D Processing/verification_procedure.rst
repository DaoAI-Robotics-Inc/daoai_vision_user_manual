Procedure of Using Verification Node
=======================================

Verification node is usually the final process of 3d object pose estimation. After the poses are verified they can be used to generate picking poses.

Steps in using verification node:
1. Compute initial 3d poses using 3d object finder node, mod finder node(3d mode), or reconstruct node, etc.
2. Use alignment node to refine 3d poses
3. Use verification node to determine which 3d poses are valid

Parameter Tunning in Depth Mode
----------------------------------------

Besides verifying if the model is closely aligned with the scene, an important feature of depth mode is to reject poses where
objects are below the scene(occluded by other objects). In application this can be used where objects with too much occlusion by other objects
can not be picked up. You can change *Occluded Part Tolerance* to determine how much occlusion to reject a pose.

Parameter Tunning in Edge Mode
------------------------------------------

Normally the edge mode produces lower verification score. Set a lower confidence if you want more poses to be kept. You can also change edge extract parameters 
and preview them in display.

Parameter Tunning in Stacking Mode
---------------------------------------------

Stacking mode calculates visibility(visible points ratio of the model) by doing a pinhole projection. Changing FOV will change the visibility of the pose,
thus change the number of poses being kept.