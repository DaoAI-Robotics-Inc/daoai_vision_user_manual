2D Mod Finder Picking
=====================

The 2D Mod Finder template is mainly composed of four well-designed flowcharts: ``Pose_Defined_3D``, ``2D_Mod_Detction``, ``Picking``, ``Pick_Pose_Generation``.



Pose_Defined_3D
----------------

This flowchart is mainly designed for loading calibration file and generating gripper position.

.. image:: Images/2dmod_pose-defined-3d.png
    :align: center
    
|


2D_Mod_Detction
----------------

This flowchart is a sub flowchart of ``Pose_Defined_3D``. It is mainly designed for detecting the precise location of object to be picked.


.. image:: Images/2dmod_detection.png
    :align: center
    
|

Picking
-------

This flowchart is mainly designed for sending generate


.. image:: Images/2dmod_picking.png
    :align: center
    
|

Pick_Pose_Generation
--------------------

This flowchart is a sub flowchart of ``Picking``. It is mainly designed for  Generating evaluated picking pose (gripper position).

.. image:: Images/2dmod_pick_pose_gener.png
    :align: center
    
|