Pose Generation node
=======================

Overview
----------

For calibration scenarios that requires the robot to move in certain ways around the working space. 

Pose Generation node can generate such poses for you and provide convenience for the calibration task.

Pose Genreation offers five common moving patterns that are often used during the calibration process.

Moving patterns that are available:

* Circle
* Square
* Board Calibration
* Gripper Check
* Sphere Calibration

Input & Output
----------

+----------------------------------------+-------------------------------+-------------------------------------------------------------------------------+
| Input                                  | Type                          | Description                                                                   |
+========================================+===============================+===============================================================================+
| Reference Pose                         | Pose                          | The reference (usually tool in base) pose to generate poses                   |
|                                        |                               | have slighly different naming for each Moving Type.                           |
+----------------------------------------+-------------------------------+-------------------------------------------------------------------------------+

+-------------------------+-------------------+------------------------------------------------------------------------+
| Output                  | Type              | Description                                                            |
+=========================+===================+========================================================================+
| poses                   | vector<Pose>      | Vector of generated poses.                                             |
+-------------------------+-------------------+------------------------------------------------------------------------+

Mode and Settings
-------------------

Circle
~~~~~~~~
   Generate a circle pattern around the center point, while keeping the object or calibration-board always facing the camera.

   - Distance: 
      The distance of object to camera.  

   - Number of Poses: 
      Number of poses to generate 

   - Tilt Angle:
      Tilt Angle (rx, ry rotation) of the gripper with respect to the camera. 

   - Height Var:
      The variation on height of the generated poses.

   - Rotation Var:
      The variation on rotation of the generated poses.

Square
~~~~~~~~
   Generate a square pattern around the center point, while keeping the object or calibration-board always facing the camera.

   - Translate X/Y/Z: 
      The X, Y, Z axis variation on the generated posese. 

Board Calibration
~~~~~~~~~~~~~~~~~~~
   Generate a Board Calibration Moving pattern. When Eye-in-hand, move the camera around the calibration-board in specified rotation angle with respect to the calibration-board.
   When Eye-to-hand, rotate the robot and calibration-board to specified rotation angle with respect to the camera.

   - Hand Eye Config:
      Choose Eye in hand or Eye to hand.

   - Camera to Board Center Dist.:
      The distance(mm) of camera to calibration board.

   - Flip Board:
      If checked, will correct the camera and calibration board flip by rotating rz 180.

   - Tilt Angle:
      The tilt Angle (rx,ry) from generated pose to ref pose. 

   - Min Z rotation:
      The minimum Z rotation in generated poses.

   - Max Z rotation:
      The maximum Z rotation in generated poses.

Gripper Check
~~~~~~~~~~~~~~~~
   Generated poses that first contain 32 poses, 26 x,y,z movement, 5 rotation movements, and another 5 for each number of rotation greater than 1.

   - Number of Rotations:
      number of rotations to generate, each have 5 poses.
   
   - Tilt Angle:
      The tile angle (rx ry rotation) from generated pose to ref pose. 

   - Translate X/Y/Z:
      The X, Y, Z axis variation on the generated posese. 

   - Min Z Rotation:
      The minimum Z rotation in generated poses.

   - Max Z Rotation:
      The maximum Z rotation in generated poses.

Sphere Calibration
~~~~~~~~~~~~~~~~~~~~
   Generated poses to rotate the gripper while keeping the sphere in the gripper in a same position. 

   - Number of Rotations:
      number of rotations to generate, each have 5 poses.

   - Tilt Angle:
      The tile angle (rx ry rotation) from generated pose to ref pose. 

   - Min Z rotation:
      The minimum Z rotation in generated poses.

   - Max Z rotation:
      The maximum Z rotation in generated poses.

Procedure to Use
------------------

1. You need Robot Read Node or other nodes to provide a reference pose to generate poses.

   .. image:: Images/pose_generation_node/step_1.png
      :scale: 80%
|

2. Insert a Pose Generation node, and select a Moving Type

   .. image:: Images/pose_generation_node/step_2.png
      :scale: 80%
|

3. Link the robot read output and input the Generate Pose settings.

   .. image:: Images/pose_generation_node/step_3.png
      :scale: 80%
|

4. Run the Pose Generations Node to output a vector of poses.

5. Write poses to robot either write the entire vector, or select a index in the vector to output.

   .. image:: Images/pose_generation_node/step_5.png
      :scale: 80%

   .. image:: Images/pose_generation_node/step_5_a.png
      :scale: 80%
|

6. You can also use a loop node and Advanced expression to output the poses one at a time. 

   .. image:: Images/pose_generation_node/step_6.png
      :scale: 80%
|

Exercise
----------

Scenario 1
~~~~~~~~~~~~
You and your partner is working on calibrating with Pose Generation Node. And your partner has run into some problems
Choose the best answer for the following questions.

1. Your partner is using circle mode to generated poses expecting that the calibration board is always facing the camera. But turns out it is facing outwards of the camera. How can you correct this?

   A. Change the Tilt Angle to negative of its current value.
   B. Change the Distance to negative of its current value.
   C. A or B
   D. B only
|
2. Your partner is using Board Calibration mode, and that the calibration-board is mounted to the wrong side (rz-180), and how can you fix this? 

   A. check Flip board
   B. Add 180 to Min Z Rotation
   C. A or B
   D. None of The above.
|
3. Your parnter is using Gripper Check mode, and want to generated 42 poses, how should you configure the settings?

   A. Change Number of Rotations to 3.
   B. Change Number of Rotations to 8.
   C. Change the Number of Rotations to 42.
   D. Cannot generate exactly 42 poses.
|
|
|
|
|

Answer
~~~~~~~~

1. C 

**Explanation**: if the the camera is facing outwards, then you should first see that the tilt angle is configured negatively to its correct value.
But also changing the distance to negative also fixes this issue. So either A or B can correct this.

2. A

**Explanation**: If Enbaled Flip Board, will add a rz 180 to all generated poses. Whereas the Min Z rotation only effects rz rotation poses. Hence A only. 

3. A 

**Explanation**: Recall that the Gripper Check mode generates 32 poses initally, and add another 5 poses for each Number of Rotations greater than 1.
Therefore, setting the Number of Rotations to 3 will add 10 poses after the inital pose, to get total of 42 poses.
