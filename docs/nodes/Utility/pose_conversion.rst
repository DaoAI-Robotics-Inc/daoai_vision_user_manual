Pose Conversion Node 
=======================

Overview
---------

Pose Conversion Node allow you to perform pose operations to convert into different datatypes.

Supported conversion modes are:
    
    - **Map to Vector**: Convert pose map to pose vector
    - **Pose 2D to 3D**: Convert 2D poses to 3D poses
    - **Vector of Pose(s)**: Convert arbituary number poses to a single vector

Input and Output
------------------

Input field is different for each Mode. 

+----------------------------------------+--------------------------------------------+--------------------------------------------------------------------------+
| Input                                  | Type                                       | Description                                                              |
+========================================+============================================+==========================================================================+
| PoseMap (Map to Vector Mode)           | MapVecPose or MapVecPose2D                 | Pose Map 3d or 2d (usually from outputs of mod finder node)              |
+----------------------------------------+--------------------------------------------+--------------------------------------------------------------------------+
| 2D Pose or Poses (Pose 2D to 3D Mode)  | Pose2D or VecPose2D or MapVecPose2D        | 2D pose (usually from outputs of 2d mod finder node)                     |
+----------------------------------------+--------------------------------------------+--------------------------------------------------------------------------+
| Pose (Vector of Poses)                 | Pose3D                                     | Can add arbituary number of single poses                                 |
+----------------------------------------+--------------------------------------------+--------------------------------------------------------------------------+

+----------------------------------+--------------------------------------------+--------------------------------------------------------------------------+
| Output                           | Type                                       | Description                                                              |
+==================================+============================================+==========================================================================+
| 2dPoseVector                     | VecPose2D                                  | Vector of 2D pose, outputs from Map to Vector mode                       |
+----------------------------------+--------------------------------------------+--------------------------------------------------------------------------+
| 3dPoseVector                     | VecPose3D                                  | Vector of 3D pose, can be outputs from all modes                         |
+----------------------------------+--------------------------------------------+--------------------------------------------------------------------------+
| SinglePose                       | Pose3D                                     | Pose 2D to 3D Mode's output when single 2d pose                          |
+----------------------------------+--------------------------------------------+--------------------------------------------------------------------------+

Procedure to Use
------------------

1. Set up Camera and Mod Finder nodes. 

2. Insert a pose conversion node.
    .. image:: Images/pose_conversion/step_2.png

3. Select a Mode: (Map to Vector, Pose 2D to 3D, or Vector of Poses).

4. Link the input, usually from mod finder node.
    .. image:: Images/pose_conversion/step_4.png

5. Run the node, and you can access the outputs in other nodes.
