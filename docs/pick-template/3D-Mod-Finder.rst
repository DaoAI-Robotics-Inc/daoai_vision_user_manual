3D Mod Finder Picking
=====================

The 3D Mod Finder template is mainly composed of four well-designed flowcharts: ``Pose_Defined_3D``, ``3D_Mod_Detction``, ``Picking``, ``Pick_Pose_Generation``.


Pose_Defined_3D
---------------

This flowchart is mainly designed for loading calibration file and generating gripper position.

.. image:: Images/3dmod_pd3d.png
    :align: center
    
|

3D_Mod_Detction
---------------

This flowchart is a sub flowchart of ``Pose_Defined_3D``. It is mainly designed for detecting the precise location of object to be picked.

.. image:: Images/3dmod_3dmd.png
    :align: center
    
|


Picking
-------

This flowchart is mainly designed for sending generated pose to robot for picking object and receiving the feedback from robot.


.. image:: Images/3dmod_picking.png
    :align: center
    
|

Pick_Pose_Generation
--------------------

This flowchart is a sub flowchart of ``Picking``. It is mainly designed for  Generating evaluated picking pose (gripper position).

.. image:: Images/3dmod_ppg.png
    :align: center
    
|











