Overview
======================

Modes 
---------------------------

* Accumulate : In this mode, the calibration node accumulates (loads) the needed data and calibration settings to be used in the final mode for calibration computation.
* Final : In this mode, the calibration node uses the data from the accumulation mode and perform the actual robot calibration.  
* Load : In this mode, the calibration node loads the output from the final mode for future use. This can help to load previous calibration results without a need to run previous modes. 

Accumulate mode inputs 
~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Pose (type:Pose) : Pose collected from robot read node. 

Accumulate mode outputs 
~~~~~~~~~~~~~~~~~~~~~~~~~~~

* pointerToHandEyeCalibration2dV02 (type:HandEyeCalibration2dV02) : This output includes the information about the calibration settings alongside with the data needed for performing calibration computation in the final mode. 
* status (type:Int) : This output indicates if there were any errors during the node execution. If the value is 0, no error has occurred. However, if the value is non-zero, an error has occurred during execution and an error message will be printed in the console.

Final mode inputs 
~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Reference node (type:String) : The reference calibration in accumulation mode which its output will be used to perform calibration. 
* File name (type:String) : The filename used to save the outputs of the node. The outputs will be saved in a file with specified name you defined in the "pin_calibrations" folder in the workspace directory.
* Number of rows (type:Int) : Number of the rows in the used chessboard that robot pin touches. Should be a positive integer. 
* Number of cols (type:Int) : Number of columns in the used chessboard that the robot pin touches. Should be a positive integer.
* Row spacing (type:Double) : The distance (mm) between each pin location on the chessboard in a row. Should be a positive double. 
* Column Spacing (type:Double) : The distance (mm) between each pin location on the chessboard in a column. Should be a positive double. 
* Use initial guess (type:Bool): The initial guess for the translation of the pin to TCP. This will be then used as optimization initialization when performing calibration computation. The translation value is zero if not set.    

Final mode outputs 
~~~~~~~~~~~~~~~~~~~~~~~~~~~

* PlaneToWorld (type:Pose) : The 3D transformation from the robot plane to world (chessboard). Note that as we are performing 2D calibration, this transformation only includes 2D components (x,y and Rz).  
* WorldToPlane (type:Pose) : The 3D transformation from world (chessboard) to robot plane. Note that as we are performing 2D calibration, this transformation only includes 2D components (x,y and Rz).
* PinToTcp (type:Pose) : The 3D translation from pin to robot TCP. Note that as we are performing 2D calibration, this translation only includes 2D components (x,y).
* pointerToHandEyeCalibration2dV02 (type:HandEyeCalibration2dV02) : This output includes the information about the calibration settings alongside with the data needed for performing calibration computation in the final mode. 
* status (type:Int) : This output indicates if there were any errors during the node execution. If the value is 0, no error has occurred. However, if the value is non-zero, an error has occurred during execution and an error message will be printed in the console.

Load mode inputs 
~~~~~~~~~~~~~~~~~~~~~~~~~~~

* File name (type:String) : The filename to load the outputs from the final mode.


Load mode outputs 
~~~~~~~~~~~~~~~~~~~~~~~~~~~

The same as the final mode.