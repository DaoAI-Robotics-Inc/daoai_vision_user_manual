2D picking
==========

The 2D Picking template is mainly composed of four well-designed flowcharts: ``Pick_Pose_Define_2D``, ``2D_Detction``, ``Picking``

Pick_Pose_Define_2D
--------------------

This flowchart is mainly designed for loading calibration file and generating gripper position.

.. image:: Images/2d_pd2d.png
    :align: center
    
|

2D_Detection
------------

It is mainly designed for detecting the precise location of object to be picked.

.. image:: Images/2d_detect.png
    :align: center
    
|



Picking
-------

This flowchart is mainly designed for sending generated pose to robot for picking object and receiving the feedback from robot.

.. image:: Images/2d_picking.png
    :align: center
    
|
