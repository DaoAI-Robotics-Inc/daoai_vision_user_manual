Quantitative calibration validation
===================================
This article describes how to quantitatively validate the correctness of the active camera's current calibration. The procedure can be performed as a sanity check just after calibrating, or at any future moment, especially if you suspect that the camera might have moved relative to the robot. It consists in performing one or more additional calibration plate detections, and computing for each detection the error with respect to the value stored during the last successful calibration.

.. tip:: The robot-camera calibration error might not be constant across the field of view. It is therefore recommended to validate the calibration as described in this article inside the Region of Interest (ROI) of the application, where picking is meant to take place.

Requirements
~~~~~~~~~~~~
Calibration validation requires a successful calibration to exist for the active camera. It also imposes a constraint on the placement of the calibration plate with respect to the robot, which depends on the camera mount:

* **Fixed camera**: The plate location with respect to the robot flange should be the exactly the same as when calibration ran.

.. image:: images/validation-camera-fixed.png
    :align: center 

* **Robot-mounted camera**: The plate location with respect to the robot base should be the exactly the same as when calibration ran.

.. image:: images/validation-camera-on-robot.png
    :align: center

|

.. warning:: The range of movements of robot will affect the calibration result, you might get a low error but not a meaningful result. Usually your range should cover the whole region of interest for future picking tasks to make the calibration result meaningful.

If you are validating just after running calibration, this contraint should not be an issue, but you might want to perform validation regularly over time, days, weeks or months after the last successful calibration. When this is the case, it is recommended to:

* **Fixed camera**: Use a (manual or automatic) tool changer, and have the calibration plate rigidly attached to one of the tool ends. It's important that the tool changer is such that the mounted tool is subject to neglectable mounting errors.

* **Robot-mounted camera**: Rigidly fix the calibration plate to a wall or other structure in the work cell. When performing validation, the plate should be at a distance to the camera similar to the distance at which parts are expected to be picked.

Validation from the calibraiton template
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
First, collect another set of calibration bag data differ from the bag data used to calibrate.

Then go to the **Test** flowchart, and you need to specify the path to the bag files you just collected in the reader node.

.. image:: images/test-flowchart.png
    :align: center

Make sure the yml file is inside the **calibrations** folder of current workspace folder.

.. image:: images/calibrations-folder.png
    :align: center

Enter the yml file name to the **calibration** node **Test** mode.

.. image:: images/yml-file-name.png
    :align: center

Then run the flowchart to see the console output. You will be able to see the error between the calibration and current validation dataset.

.. image:: images/console-print.png
    :align: center

|

Sphere Calibration Validation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Quantitative calibration validation is not supported yet. Please use :ref:`Qualitative calibration validation`.

Invalid robot-camera calibration?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
If the outcome of calibration validation is that the current calibration is invalid, the most likely cause is that the camera moved with respect to the robot base (fixed camera) or robot flange (camera on robot). When this is the case, robot-camera calibration needs to be performed again.

If the camera has not moved with respect to the robot, it could be that something went unexpectedly wrong during calibration. The following pointers can help you identify the cause:

* The calibration plate moved during the calibration process.
* The camera mount (fixed or robot-mounted) was incorrectly selected in the calibration wizard.
* The calibration poses don't comply with the recommendations.
* If you are integrating a new robot brand with DaoAI Vision Studio, there might be an incompatability in the way poses are communicated between DaoAI Vision and the robot. Especially the euler order and magnitude for the translation. 
