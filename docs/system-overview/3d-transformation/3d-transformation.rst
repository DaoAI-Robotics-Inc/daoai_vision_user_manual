3D Transformation Concept
=========================
To use Vision Studio, some concepts of 3D transformation are necessary.

Pose and Transformation
-----------------------

Pose stands for the position and rotation.
    .. image:: Images/3d-right-hand.png 
        :scale: 70 %

**Position** is usually represented by right hand rule, and R/G/B stands for X/Y/Z.

**Rotation** is represented by Euler angles(Rx, Ry, Rz) or Quaternions (a, b, c, w). Vision Studio use Euler angles by default.

A transformation or pose of target (A) coordinate in reference (B) coordinate is represented by A in B .

.. hint:: For example, **Obj** initially is at the origin of reference  coordinate (B) which is (0, 0, 0, 0, 0, 0), and we move the **Obj** to the position [100,100,50]. Afterwards, we rotate the **Obj** along it's **X** axis for 60 degree. The final pose of **Obj** is [100, 100, 50, 60, 0, 0]. 
        
    .. image:: Images/3d-pose-example.png
        :scale: 80 %
.. caution:: Talking about the orientation, we usually use Euler order to represent the orientation. Ane euler angle will need to have a specified rotation order. Different robot may have different conventions, for example ABB robot used the ZYX sequence. For more details, refer to the `page <https://en.wikipedia.org/wiki/Euler_angles>`_ 

Sources of pose and transformation in Vision Studio:
 * Robot Read
 * Calibrations (Calibration, Sphere Calibration, DA Calibration)
 * Detection nodes (Mod Finder, Reconstruct, Box Volume Estimation, Alignment)
 * Manually Define (Assemble Pose, Gripper)

Transformation Tree
-------------------

Transformation Tree is using known poses and transformations to calculate the unknowns.
    .. image:: Images/3d-transformation-tree.png
        :scale: 60 %

.. important:: The process of detection, calibration and robot guidance all serves the core **Transformation Tree**, so understanding it's concept is the very important.

How to Establish a Transformation Tree?
"""""""""""""""""""""""""""""""""""""""
In the figure below, there are five objects ABCDE, and some of the relative positions are known, and constructed a transformation chain(Purple).

Known transformations: [A in World] [E in A] [D in World] [C in D] [B in C]
    .. image:: Images/3d-transformation-tree-example1.png
        :scale: 50 %

Then the transformation between any two objects in the **same** transformation chain can be computed by transformation tree.

[B in E] or [D in A] etc. are all in the same transformation chain thus able to be computed.
    .. image:: Images/3d-transformation-tree-example2.png
        :scale: 50 %

However, if two objects are **not** in the same transformation chain, their transformation cannot be computed. To be able to calculate the transformation, the transformation chain must be connected first.

B and E are not in the same transformation chain.
    .. image:: Images/3d-transformation-tree-example3.png
        :scale: 50 %

To acquire [B in E], first acquire any transformation that will make B and E be in the same transformation chain.

For an example, [C in A].
    .. image:: Images/3d-transformation-tree-example4.png
        :scale: 50 %

