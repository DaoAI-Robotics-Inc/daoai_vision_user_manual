3D Transformation Concept
=========================
To use Vision Studio, some concepts of 3D transformation are necessary.

Pose and Transformation
-----------------------

Pose stands for the position and rotation.
    .. image:: images/3d-right-hand.png 
        :scale: 70 %

**Position** is usually represented by right hand rule, and R/G/B stands for X/Y/Z.

**Rotation** is represented by Euler angles(Rx, Ry, Rz) or Quaternions (a, b, c, w). Vision Studio use Euler angles by default.

A transformation or pose of target coordinate in reference coordinate is represented by A in B .

.. hint:: For an example, **Obj** is at the origin of reference coordinate which is (0, 0, 0, 0, 0, 0), and after transformation [**Obj'** in **Obj**] = [100, 100, 50, 60, 0, 0]
    
    .. image:: images/3d-pose-example.png
        :scale: 80 %
    
Sources of pose and transformation in Vision Studio:
 * Robot Read
 * Calibrations (Calibration, Sphere Calibration, DA Calibration)
 * Detection nodes (Mod Finder, Reconstruct, Box Volume Estimation, Alignment)
 * Manually Define (Assemble Pose, Gripper)

Transformation Tree
-------------------

Transformation Tree is useing known poses and trasnformations to calculate the unknowns.
    .. image:: images/3d-transformation-tree.png
        :scale: 60 %

.. important:: The process of detection, calibration and robot guidiance all serves the core **Transformation Tree**, so understanding it's concept is the very important.

How to Establish a Transformation Tree?
"""""""""""""""""""""""""""""""""""""""
In the figure below, there are five objects ABCDE, and some of the relative positions are known, and constructed a transformation chain(Purple).

Known trasnformations: [A in World] [E in A] [D in World] [C in D] [B in C]
    .. image:: images/3d-transformation-tree-example1.png
        :scale: 50 %

Then the transformation between any two objects in the **same** transformation chain can be computed by transformation tree.

[B in E] or [D in A] etc. are all in the same transformation chain thus able to be computed.
    .. image:: images/3d-transformation-tree-example2.png
        :scale: 50 %

However, if two objects are **not** in the same transformation chain, their transformation cannot be computed. To be able to calculate the transformation, the transformation chain must be connected first.

B and E are not in the same transformation chain.
    .. image:: images/3d-transformation-tree-example3.png
        :scale: 50 %

To aquire [B in E], first aquire any transformation that will make B and E be in the same transformation chain.

For an example, [C in A].
    .. image:: images/3d-transformation-tree-example4.png
        :scale: 50 %

