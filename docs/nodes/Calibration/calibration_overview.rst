Overview
==========================

Modes 
-------------------------

* Accumulate : In this mode, the calibration node accumulates (loads) the needed data and calibration settings to be used in the final mode for calibration computation.
* Final : In this mode, the calibration node uses the data from the accumulation mode and perform the actual robot calibration.  
* Load : In this mode, the calibration node loads the output from the final mode for future use. This can help to load previous calibration results without a need to run previous modes. 


Accumulate mode inputs 
--------------------

* Hand Eye Config (type:Int) : Robot camera configuration. Either eye-to-hand (calibration tool mounted on robot) or eye-in-hand (camera mounted on robot).
* Pose (type:Pose) : Pose collected from robot read node. 
* Image (type:Image) : Image captured from the calibration tool.
* Point Cloud (type:Cloud) : Cloud captured from the calibration tool. This should be set if you are using the point cloud for calibration.
* Use Point cloud (type:Bool): Option to use input point cloud for calibration or not. 
* Grid Type (type:Int) : The used type of calibration tool. It can be either chessboard or grid circles. 
* Number of rows (type:Int) : The number of rows in the grid board. 
* Number of columns (type:Int) : The number of columns in the grid board. 
* Row spacing (type:Double) : The distance (mm) between every two square corners in a row in the chessboard or the distance between every two circles in a row in the circle grid. 
* Column spacing (type:Double) : The distance (mm) between every two square corners in a column in the chessboard or the distance between every two circles in a column in the circle grid.
* Use large circle orientation (type:Bool): Option to either use large circle orientation for calibration or not. This option is available if only you are using circle grids as the calibration tool. This option gives flexibility in how much the grid can be rotated. 
 
Accumulate mode outputs 
~~~~~~~~~~~~~~~~~~~~~~~~~~~

* pointerToCalibration (type:Calibration) : This output includes the information about the calibration settings alongside with the data needed for performing calibration computation in the final mode. 
* status (type:Int) : This output indicates if there were any errors during the node execution. If the value is 0, no error has occurred. However, if the value is non-zero, an error has occurred during execution and an error message will be printed in the console.

Final mode inputs 
~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Camera intrinsic (type:CameraIntrinsic) : Camera intrinsic. This input is optional. If not set, the camera intrinsic will be obtained using the data loaded in the accumulate mode. 
* Reference node (type:String) : The reference calibration node in accumulation mode which its output will be used to perform calibration. 
* Cost function (type:Int) :  The used cost function for calibration computation. 
* File name (type:String) : The filename used to save the outputs of the node in. This file is saved in the folder 'calibrations' in the workspace folder.

Final mode outputs 
~~~~~~~~~~~~~~~~~~~~~~~~~~~

* cam_in_gripper (type:Pose) : The 3D transformation from the camera to the gripper (TCP). Only has value in eye-in-hand situaltions.
* base_in_world (type:Pose) : The 3D transformation from robot base to the world (calibration board). Only has value in eye-in-hand situaltions.
* cam_in_base (type:Pose) : The 3D transformation from camera to robot base. Only has value in eye-to-hand situations.
* gripper_in_world (type:Pose) : The 3D transformation from gripper (TCP) to world (calibration board). Only has value in eye-to-hand situations.
* pointerToCalibration (type:Calibration) : This output includes the information about the calibration settings alongside with the results of the calibration from the final mode. 
* status (type:Int) : This output indicates if there were any errors during the node excecution. If the value is 0, no error has occured. However, if the value is non-zero, an error has occurred during execution and an error message will be printed in the console.

Load mode inputs 
~~~~~~~~~~~~~~~~~~~~~~~~~~~

* File name (type:String) : The filename to load the outputs from the final mode.

Load mode outputs 
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Same as the final mode. 