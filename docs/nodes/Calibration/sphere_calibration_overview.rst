Overview
=====================

Modes 
------------------------------

* Accumulate : In this mode, the calibration node accumualtes (loads) the needed data and calibration settings to be used in the final mode for calibration computation.
* Final : In this mode, the calibration node uses the data from the accumulation mode and perfrom the acutal robot calibration.  
* Load : In this mode, the calibration node loads the ouput from the final mode for future use. This can help to load previous calibration results without a need to run previous modes. 

Accumulate mode inputs 
~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Hand Eye Confg (type:Pose) : Robot camera configuration. Either eye-to-hand (sphere mounted on robot arm) or eye-in-hand (camera mounted on robot).
* Robot Pose (type:Pose) : Robot pose (TCP in base).  
* Sphere Pose (type:Pose) : Pose of detected spheres.
* Use Intitial guess (type:Bool) : An option to set the initial value for the translation of gripper (TCP) to camera in eye-in-hand scenario or the translation of sphere in gripper (TCP) in eye-to-hand scenario.

Accumulate mode outputs 
~~~~~~~~~~~~~~~~~~~~~~~~~~~

* pointerToSphereCalibration (type:SphereCalibration) : This output includes the inforamtion about the calibration settings alongside with the data needed for performing calibration computation in the final mode. 
* status (type:Int) : This output indicates if there were any erros during the node excecution. If the value is 0, no error has occured. However, if the value is non-zero, an error has occured during excecution and an error message will be printed in the console.


Final mode inputs 
~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Reference node (type:String) : The reference calibration node in accumulation mode which its output will be used to perform calibration. 
* File name (type:String) : The filename used to save the outputs of the node in. This file is saved in the folder 'sphere_calibrations' in the workspace folder.


Final mode outputs 
~~~~~~~~~~~~~~~~~~~~~~~~~~~

* gripper_in_cam (type:Pose) : The 3D transformation from the gripper (TCP) to camera. Only has value in eye-in-hand situaltions.
* cam_in_gripper (type:PPose) : The 3D transformation from the camera to gripper (TCP). Only has value in eye-in-hand situaltions. 
* sphere_in_base (type:PPose) : The 3D translation from sphere to robot base. Only has value in eye-in-hand situaltions. 
* base_in_cam (type:Pose) : The 3D transformation from robot base to camera . Only has value in eye-to-hand situaltions. 
* cam_in_base (type:PPose) : The 3D transformation from camera to robot base. Only has value in eye-to-hand situaltions.
* sphere_in_gripper (type:Pose) : The 3D transformation from sphere to the gripper (TCP). Only has value in eye-to-hand situaltions. 
* pointerToSphereCalibration (type:SphereCalibration) : This output includes the inforamtion about the calibration settings alongside with the data needed for performing calibration computation in the final mode. 
* status (type:Int) : This output indicates if there were any erros during the node excecution. If the value is 0, no error has occured. However, if the value is non-zero, an error has occured during excecution and an error message will be printed in the console.


Load mode inputs 
~~~~~~~~~~~~~~~~~~~~~~~~~~~

* File name (type:String) : The filename to load the outputs from the final mode.

Load mode outputs 
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Same as the final mode. 
