Calibration node
==========================

This node perfrorms 3D robot calibration using chessboard or circle grid as the calibration tool. This node can be run in three different modes.  

Overview
------------------------

Modes 
~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Accumulate : In this mode, the calibration node accumualtes (loads) the needed data and calibration settings to be used in the final mode for calibration computation.
* Final : In this mode, the calibration node uses the data from the accumulation mode and perfrom the acutal robot calibration.  
* Load : In this mode, the calibration node loads the ouput from the final for future use. This can help to load previous calibration results without a need to run previous modes. 


Accumulate mode inputs 
~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Hand Eye Confg (type:Int) : Robot camera configuration. Either eye-to-hand (calibration tool mounted on robot) or eye-in-hand (camera mounted on robot).
* Pose (type:Pose) : Pose collected from robot read node. 
* Image (type:Image) : Image captured from the calibration tool.
* Point Cloud (type:Cloud) : Cloud captured from the calibration tool. This should be set if you are using the point cloud for calibration.
* Use Point cloud (type:Bool): Option to use input point cloud for calibration or not. 
* Grid Type (type:Int) : The used type of calibration tool. It can be either chessboard or grid circles. 
* Number of rows (type:Int) : The number of rows in the grid board. 
* Number of columns (type:Int) : The number of columns in the grid board. 
* Row spacing (type:Double) : The distance (mm) between every two square corners in a row in the chessboard or the distance between every two circles in a row in the circle grid. 
* Column spacing (type:Double) : The distance (mm) between every two square corners in a column in the chessboard or the distance between every two circles in a column in the circle grid.
* Use large circle oreintation (type:Bool): Option to either use large circle orientation for calibration or not. This option is available if only the user is using circle grids as the calibration tool. This option gives flexibility in how much the grid can be rotated. 
 
Accumulate mode outputs 
~~~~~~~~~~~~~~~~~~~~~~~~~~~

* pointerToCalibration (type:Calibration) : This output includes the inforamtion about the calibration settings alongside with the data needed for performing calibration computation in the final mode. 
* status (type:Int) : This output indicates if there were any erros during the node excecution. If the value is 0, no error has occured. However, if the value is non-zero, an error has occured during excecution and an error message will be printed in the console.

Final mode inputs 
~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Camera intrinsics (type:CameraIntrinsics) : Camera intrinsics. This input is optional. If not set, the camera intrinsics will be obtained using the data loaded in the accumulate mode. 
* Reference node (type:String) : The reference calibration node in accumulation mode which its output will be used to perform calibration. 
* Cost function (type:Int) :  The used cost function for calibration computation. 
* File name (type:String) : The filename used to save the outputs of the node in. This file is saved in the folder 'calibrations' in the workspace folder.

Final mode outputs 
~~~~~~~~~~~~~~~~~~~~~~~~~~~

* cam_in_gripper (type:Pose) : The 3D transformation from the camera to the gripper (TCP). Only has value in eye-in-hand situaltions.
* base_in_world (type:Pose) : The 3D transformation from robot base to the world (calibration board). Only has value in eye-in-hand situaltions.
* cam_in_base (type:Pose) : The 3D transformation from camera to robot base. Only has value in eye-to-hand situations.
* gripper_in_world (type:Pose) : The 3D transformation from gripper (TCP) to world (calibration board). Only has value in eye-to-hand situations.
* pointerToCalibration (type:Calibration) : This output includes the inforamtion about the calibration settings alongside with the results of the calibration from the final mode. 
* status (type:Int) : This output indicates the if there were any erros during the node excecution. If the value is 0, no error has occured. However, if the value is non-zero, an error has occured during excecution and an error message will be printed in the console.

Load mode inputs 
~~~~~~~~~~~~~~~~~~~~~~~~~~~

* File name (type:String) : The filename to load the outputs from the final mode.

Load mode outputs 
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Same as the final mode. 

Procedure for Using Calibration Node
------------------------------------------

In order to perfrom calibration using this node, we need to capture camera images of the calibration tool from different views. The calibration tools that can be used in this node are grid circles and gird chessboards that examples of each are shown below. 

.. image:: Images/calibration_node/chessboard.jpg
    :align: center
    
|

.. image:: Images/calibration_node/circleboard.jpg
    :align: center
    
|
 
Note that the captured images should contain a variety of images with differnt position and rotation angles to ensure a good calibration result. Once you have captured calibrartion images, you can add the calibration node into the flowchart to perfrom calibration. (Templates provided in the software)
When adding this node to the flowchart, you will see the option for choosing the calibration mode. We provide three modes for the calibration node.
First, the accumulation mode is used to load the captured images, poses and point clouds from the calibration board and detect the corner points (chessboard) or circle center points (circle borad). When you choose the accumulation mode, you will be able to set differnt options and inputs. 

 .. image:: Images/calibration_node/accumulation.jpg
    :align: center
    
| 

 .. image:: Images/calibration_node/accumulation1.jpg
    :align: center
    
|

As shown in the above image, the user has to choose the hand-eye configuration. Also, the other inputs include the captured image, robot pose (base in gripper) and point cloud for each robot position. In addition, the user has to choose the used grid board type (calibration tool). Note that you can see the result of the 
acculumation node (detected points) by clicking on the node. In case the algorithm is not able to detect the corner/circle points, the image will be skipped and not used for final calbbration. 


After obtaining the corner/circle points, it is time to use the results and inputs from the accumulation mode to perform robot-camera calibration. This can be done by adding another calibraion node in the flowchart and setting the mode to the final mode. The final mode will perfrom the main computation for the calibration.

 .. image:: Images/calibration_node/final.jpg
    :align: center
    
|

In the final node, the user has to specify the reference accumulation node, so, the results then can be used for calibration. Also, as the calibration algorithm will use an optimization based method to obtain the calibration results, 
the user needs to choose the used cost function. In case of using a 3D camera and 3D picking, it is a better option to use the RPDepth cost function as our experiments show better results for this cost function. However, note that when using RPDepth, you will need to set the option "using the point cloud" in the accumulation mode. By running
the calibration node in the final mode, the calibration results will be obtained. More specifically, the main outputs of the final mode are the camera to gripper and base to board 3D transformations in the eye-in-hand scenario. This will be camera to base and gripper to board 3D transfromations in the eye-to-hand scenario. These transformations then can 
be used in the picking flowchart for differnt robot picking operations.


Another existing mode for calibration mode is the load mode which simply loads the result file saved in the final mode. This can be used to visualize the result of the calibration without a need to run the previous nodes. 

 .. image:: Images/calibration_node/load.jpg
    :align: center
    
|
