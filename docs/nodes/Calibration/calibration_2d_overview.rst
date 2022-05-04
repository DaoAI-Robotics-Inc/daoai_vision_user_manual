Overview
==================

Modes 
-----------------------

* Calibrate : In this mode, camera-world calibration is performed. Note that the used camera is 2D and no point cloud is used.  
* Project : In this mode, the output of the Calibrate mode is used to convert a 2D pixel location detected by a mod_finder to the 3D camera coordinates.

Calibrate mode inputs 
---------

* Image (type:Image) : Image captured from the calibration tool (chessboard or circle grid).
* Camera intrinsic (type:CameraIntrinsic) : Camera intrinsic. This input is optional. If not set, the camera intrinsic will be obtained.  
* Grid Type (type:Int) : The used type of calibration tool. It can be either chessboard or circle grid. 
* Number of rows (type:Int) : The number of rows in the grid board. 
* Number of columns (type:Int) : The number of columns in the grid board. 
* Row spacing (type:Double) : The distance (mm) between every two square corners in a row in the chessboard or the distance between every two circles in a row in the circle grid. 
* Column spacing (type:Double) : The distance (mm) between every two square corners in a column in the chessboard or the distance between every two circles in a column in the circle grid.
* Half Window Size (type:Double) : The size of the window (mm) to detect the chessboard corners. Usually set as the half size of the column/row spacing. Only used when the used grid type is chessboard.   

Calibrate mode outputs 
---------

context (type:SCalibration2dContext) : 2D calibration results including the camera intrinsic and the world (calibration tool) to camera 3D transformation (includes only 2D components). This would then be used in the project mode.

Project mode inputs 
---------

* Image (type:Image) : Image captured from the calibration tool (chessboard or circle grid).
* Mod Finder Results (type:MapSModResultData) : The result of the mod_finder node which includes the 2D orientation and pixel location (usually center point) of the detected model.
* Reference Node (type:String) : The reference calibration_2d node in calibrate mode which its output will be used in the project mode.  
* Z Offset (type:Double) : The distance (mm) from the detection surface to the calibration surface. For example, if the detection surface is below the calibration surface for 20mm, you should input 20 and vice-versa.  

Project mode outputs 
---------

poses (type:Map<Vec<Pose>>) : The 3D poses in camera coordinate system of the 2D pixels detected by mod_finder node.  
