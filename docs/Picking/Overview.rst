Overview
========

Vision does not only detect objects, but also generates the pose for robot to pick them. While the Detection flowchart generates object location, the Picking flowchart consider everything that revolves around how to pick a detected object: Which tool will it use? What pose is robot going to pick it? Is the pose collision free?

Calibration
-----------
Hand Eye calibration, where ``Hand`` stands for the robot and ``Eye`` stands for the camera, is the process where the camera and the robot learn their relative position with respect to each other. If done correctly, the camera will be able to guide the robot to correct positions in the physical environment. Calibration can be performed once the camera and robot are set to fixed position. If the camera relative position to the robot base has not moved, or vise versa, then this process does not need to be done again.

There are four general types of calibration:

* :ref:`sphere-calibration` 
* :ref:`chessboard-calibration` 
* :ref:`2d-calibration` 
* :ref:`converyor-calibration` 

Detection
---------
Detection is the process where camera and objects learn their relative positions.

There are three general detection methods, each optimized for different types of object.

* :ref:`deep-learning-segmentation`


* :ref:`mod-finder`


* :ref:`shape-finder`


