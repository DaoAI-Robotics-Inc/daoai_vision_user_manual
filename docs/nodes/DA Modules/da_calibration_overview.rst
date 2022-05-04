Overview
===================

Modes 
---------------

* Accumulate : In this mode, the calibration node accumulates (loads) the needed data and calibration settings to be used in the final mode for calibration computation.
* Final : In this mode, the calibration node uses the data from the accumulation mode and perform the actual robot calibration.  
* Load : In this mode, the calibration node loads the ouput from the final for future use. This can help to load previous calibration results without a need to run previous modes. 


Accumulate mode inputs 
-------------------------

* Hand Eye Confg (type:Int) : Robot camera configuration. Either eye-to-hand (calibration tool mounted on robot) or eye-in-hand (camera mounted on robot).
* Pose (type:Pose) : Pose collected from robot read node. 
* Image (type:Image) : Image captured from the calibration tool.
* Grid Type (type:Int) : The used type of calibration tool. It can be either chessboard or grid circles. 
* Number of rows (type:Int) : The number of rows in the grid board. 
* Number of columns (type:Int) : The number of columns in the grid board. 
* Row spacing (type:Double) : The distance (mm) between every two square corners in a row in the chessboard or the distance between every two circles in a row in the circle grid. 
* Column spacing (type:Double) : The distance (mm) between every two square corners in a column in the chessboard or the distance between every two circles in a column in the circle grid.
 
Accumulate mode outputs 
---------------------------

* milCalibrationID (type:MIL_ID) : This output includes the information about the calibration settings alongside with the data needed for performing calibration computation in the final mode. 
* calibrationStatus (type:Int) : This output indicates if there were any errors during the node execution. If the value is 0, no error has occurred. However, if the value is non-zero, an error has occurred during execution and an error message will be printed in the console.

Final mode inputs 
-----------------------

* Hand Eye Confg (type:Int) : Robot camera configuration. Either eye-to-hand (calibration tool mounted on robot) or eye-in-hand (camera mounted on robot).
* Reference node (type:String) : The reference calibration node in accumulation mode which its output will be used to perform calibration. 
* File name (type:String) : The filename used to save the outputs of the node in. This file is saved in the folder 'da_calibrations' in the workspace folder.

Final mode outputs 
------------------------

* cam_in_gripper (type:Pose) : The 3D transformation from the camera to the gripper (TCP). Only has value in eye-in-hand situations.
* base_in_world (type:Pose) : The 3D transformation from robot base to the world (calibration board). Only has value in eye-in-hand situations.
* cam_in_base (type:Pose) : The 3D transformation from camera to robot base. Only has value in eye-to-hand situations.
* gripper_in_world (type:Pose) : The 3D transformation from gripper (TCP) to world (calibration board). Only has value in eye-to-hand situations.
* milCalibrationID (type:MIL_ID) : This output includes the information about the calibration settings alongside with the data needed for performing calibration computation in the final mode. 
* calibrationStatus (type:Int) : This output indicates if there were any errors during the node execution. If the value is 0, no error has occurred. However, if the value is non-zero, an error has occurred during execution and an error message will be printed in the console.

Load mode inputs 
----------------------------

* Hand Eye Confg (type:Int) : Robot camera configuration. Either eye-to-hand (calibration tool mounted on robot) or eye-in-hand (camera mounted on robot).
* File name (type:String) : The filename to load the outputs from the final mode.

Load mode outputs 
---------------------------

Same as the final mode. 