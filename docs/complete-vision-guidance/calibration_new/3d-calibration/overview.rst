3D Calibration 
==============

Robot-camera calibration is the process where the **camera** and the **robot** learn their relative position with respect to each other, which allows the camera to guide the robot to correct positions in the work cell.

Calibration can be performed once the camera and robot have been mounted in the work cell, and needs to be redone if the camera moved relative to the robot base (fixed camera) or flange (robot mounted camera).

DaoAI ships with a calibration plate that has circles printed on it (below left) and a sphere. During robot-camera calibration, the robot shows this plate or the sphere to DaoAI Vision from different viewpoints, and DaoAI Vision learns the relative position between camera and robot:

* For a **fixed camera mount** (below center), the plate is attached to the robot end-effector, and DaoAI Vision learns the location between the camera and the robot base.
* For a **robot-mounted camera** (below right), the plate is located at a fixed position in the work cell, and DaoAI Vision learns the location between the camera and the robot flange.

.. image:: images/calibration-overview.png
    :align: center

|

Calibration uses the color image in addition to 3D information to detect the plate or the sphere, so it's important for the circles in the plate or the sphere to be clearly visible, without reflections, artifacts or over-illumination from external light sources learn more. 

The calibration board point cloud should look like image below.

.. image:: images/good-circle-board-pcd.png
    :align: center

The sphere point cloud should look like the image below, having at least 1/3 of the ball showing.

.. image:: images/sphere-cloud.png
    :align: center

|

Perform Calibration
~~~~~~~~~~~~~~~~~~~

The most accurate results are obtained when the calibration target is detected from multiple viewpoints.

There are two types of calibration supported:

* Circle board calibration 
* Sphere calibration

Circle board calibration is suitable for situations where you can mount the calibration board on the robot end-effector easily, or you want to perform eye-in-hand calibration.

.. image:: images/circle-board.png
    :align: center

|

Sphere calibration is suitable for situations when mounting the calibration board on the end-effector is hard, or you have mounted a tool on the end-effector already, and you don't want to remove the tool. In this situations, you could easily attach the sphere.

.. image:: images/sphere-cali.png
    :align: center

|

Validating calibration
~~~~~~~~~~~~~~~~~~~~~~

An **incorrect** or **outdated** calibration can lead to unexpected robot motions. An incorrect calibration can result from not following correctly the calibration prodecure. A calibration can become outdated if the camera displaced relative to the robot since the last successful calibration.

.. note:: The robot-camera calibration quality relies on the :ref:`Robot Accuracy` and on the :ref:`Camera Accuracy`. Therefore, if you observe a persistent robot-camera calibration error that cannot be fixed with better calibration poses, it is recommended to verify the accuracy of both camera and robot.

There are two ways in which robot-camera calibration can be validated:

* :ref:`Quantitative calibration validation`, using the DaoAI calibration template with corresponding robot program.
* :ref:`Qualitative calibration validation`, using the DaoAI calibration template and manual inspection.

.. Attention:: The first picks after performing calibration should be executed at a **low robot speed**, so unexpected behavior can be identified early enough to prevent the robot from colliding with people or the environment.




