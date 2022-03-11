Circle Board Calibration
=============

Circle board calibration is the recommended method for performing robot-camera calibration in Pickit. With this method, the robot shows the calibration plate to Pickit from different viewpoints.

.. tip:: You can learn about the main ideas behind multi poses robot-camera calibration by watching this video tutorial (To add).

The placing of the calibration plate and the poses from which it is detected depend on the camera mount.

Fixed camera mount
===========

If the camera is fixed to a static structure, the calibration plate must be attached to the robot flange. It does not matter how the plate is mounted, as long as it’s rigidly attached to the flange (TO ADD A LINK). It can be, for instance, directly attached to the flange (below left) or grasped by the robot gripper (below right). You should not attach it, for instance, to a suction cup with flexible bellows, as the plate will wobble.

The calibration poses are such that:

* The calibration plate is at a distance to the camera similar to the distance at which parts are expected to be picked.
* The calibration plate can be correctly detected.(TO ADD A LINK)
* The poses are distinct enough to produce an accurate calibration.
* The order in which the poses are captured is not important.

DaoAI recommends collecting the ten poses shown below to obtain an accurate calibration. It is however allowed to collect a different amount of poses, as long as their quality is good enough.

* The first four poses capture variation in plate position:
.. image:: Images/camera_fixed_position_poses.png
    :width: 100%
    :align: center 
* The next two poses capture variation in the camera-facing rotation of the plate:
.. image:: Images/camera_fixed_camera_facing_rotation_poses.png
    :width: 100%
    :align: center  
* The last four poses capture variation in plate tilt:
.. image:: Images/camera_fixed_tilt_poses.png
    :width: 100%
    :align: center 

Robot mounted camera
=======
(COPY THE SAME CONTENT AS PICKIT)    [https://docs.pickit3d.com/en/latest/documentation/calibration/multi-poses-calibration.html#calibrating-from-the-web-interface]

Calibrate from DaoAI calibration template
=============

To perform a new calibration, open the DaoAI Vision Studio, create a workspace out from the **Chessboard Calibration (To Verifiy the name)** template, and following the steps below: (Use the new process mentioned here, https://daoai.atlassian.net/jira/software/projects/DV/boards/7?assignee=612fb8249976c30069458dbf&selectedIssue=DV-549 with the current approach 1)

1. Config the calibration parameters, set blabla
2. set the robot poses in the robot script
3. Collect calibration bag files 
4. Run calibration flowchart  
5. Validate calibration result


Create workspace and set up calibration (step 1 above)
~~~~~~~~~~~~~~~~~~
Create workspace from template, and based on situation config the flowchart blabla

Set robot poses (Step 2 above)
~~~~~~~~~~~~~~
Start to run the flowchart to preview all the poses; Preview each pose;
Refer to Robot Section/Calibration program;  Setup each calibration poses. 

Collect calibration bag files (Step 3 above)
~~~~~~~~~~~~

Modify the name of the stored folder, run the robot program, remember to setup correctly the ip etc..  

Run calibration flowchart
~~~~~~~~~~~~

Run the calibration with the collected files, and store the calibraiton result out into the disk

Validating the calibration result
~~~~~~~~~~~
After you run the calibration, you will see a printed error. And to better validate the result, refer to the validating calibration result page.









