Qualitative calibration validation
================

.. attention:: This validation method relies on a human operator visually confirming the correctness of a calibration, hence is a coarse check. 
    
    DaoAI also allows to perform a quantitative calibration, which is more accurate, and recommended for applications that need to keep an eye on sources of picking errors.

Quantitative valiate the result means we are projecting back some known objects back to the cloud, and compare it with what we actually see from the camera. Following are general steps:

1. Collect validating bag data
2. Config the flowchart, and run dedicated flowchart to check the visual result

Collect validating bag data
~~~~~~~~~~

Open the same workspace for running the calibration, and set the robot pose to different ones, and collect a group of validating data. 

Eye-to-hand Gripper visulization
~~~~~~~~~~~~~~~~~


Pin visualization 
~~~~~~~~~~
1. Eye-in-hand 
2. Eye-to-hand 

Sphere visualization
~~~~~~~
Not recommended


Invalid robot-camera calibration?
~~~~~~~~~~~~~~
To add as the pickit does 