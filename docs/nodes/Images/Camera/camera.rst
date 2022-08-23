Camera Node
========================

Overview
---------

The camera node allows user to connet DaoAI Vision with a physical or virtual camera,
from which the image data can be read and used by other nodes.

Input and Output 
----------------

..|br| raw:: html

	<br>

+----------------+------------------+----------------------------------------------------------------------------------------------------+
| Input          | Type             | Description                                                                                        |
+================+==================+====================================================================================================+
| Camera Source  | Camera Name      | Selected from a list of Camera Names added in Platform Configuration                               |
+----------------+------------------+----------------------------------------------------------------------------------------------------+

+----------------+------------------+--------------------------------------------------------------------------------------------------------+
| Output         | Type             | Description                                                                                            |
+================+==================+========================================================================================================+
| image          | Image            | Captured image                                                                                         |
+----------------+------------------+--------------------------------------------------------------------------------------------------------+
| pointCloud     | Cloud            | Captured point cloud                                                                                   |
+----------------+------------------+--------------------------------------------------------------------------------------------------------+
| DepthMap       | Image            | | A depth image converted from point cloud. has been normalized, so it do not contain absolute depth   |
|                |                  | | information. can be used for depth comparison and visualization, we cannot use it as a depth map.    |        
+----------------+------------------+--------------------------------------------------------------------------------------------------------+
| intrinsicParam | CameraIntrinsics | The camera intrinsic of camera.                                                                        |
+----------------+------------------+--------------------------------------------------------------------------------------------------------+


Node Settings
-------------
The following screen shot demonstrate camera node settings

.. image:: images/camera-node-settings.png
	:scale: 100%

- **Open Platform Config**: Click to open the Platform Config where you can add and connect cameras.

- **Continuous Mode**: Toggle continuous mode, when toggled, running the Camera node will continuously capture image until user stop.

- **Continuous Mode Timeout**: The time interval which the program should wait between continuous image captures.

.. On master: - **Enable Logging**: Toggle logging option, when toggled, an output file will be written to [Workspace_dir]/Log.

Procedure to Use
----------------

1. Right click the '+' sign and click 'Insert Node'.

.. image:: images/camera-step-1.png
	:scale: 100%

2. Select Camera node and click OK.

.. image:: images/camera-step-2.png
	:scale: 100%

3. Click Platform Config and add Camera by clicking the '+' sign and then click accept.

.. image:: images/camera-step-3.png
	:scale: 100%

4. Connect to a physical or virtual camera

- 4.1. Connect to a physical camera: 
	1. Leave the virtual Camera checkbox unchecked. 
	2. You may optionally check the 'save camera data' checkbox if you wish to also save the camera data to your file. 
	3. You may check the 'Enable Remote Camera' if your camera is connected through network.
	4. Click Update camera List
	5. Click the expand arrow in Serial number or IP and select your camera from the list.
	6. You can choose to load an optional camera configuration (.cfg) file generated through DaoAI Camera Studio. 
	7. click connect.
	8. click Apply.

	.. image:: images/camera-step-4-1.png
	:scale: 100%

- 4.2. connect to a virtual camera
	1. Check the virtual camera checkbox.
	2. Select "From File" to load a single file.
	3. Click browse to select file.
	4. Click Apply

	.. image:: images/camera-step-4-2.png
		:scale: 100%

	- 4.2.1. Select From Folder to load all files from folder, the camera node will read image sequencially in the folder

		.. image:: images/camera-step-4-2-1.png
			:scale: 100%

	- 4.2.2. Select From Numbered Files, and select a folder path, specifiy the file prefix and start/end index. 
	The camera node will read image sequencially in the folder for filenames began with the speicified prefix and ordered by their index. 

		.. image:: images/camera-step-4-2-2.png
			:scale: 100%

5. 1.Close the Platform Configuration window, 2.select camera Source

	.. image:: images/camera-step-5.png
			:scale: 100%

6. Select the camera node if its not selected already, click run select node, and you should be able to see the image on the left view port.

	.. image:: images/camera-step-6.png
			:scale: 100%

Excercise
---------

Here's a `link to .dcf file <https://daoairoboticsinc-my.sharepoint.com/:u:/g/personal/tzhang_daoai_com/EUaL8LFp-JlJugrB-VYSCr8BODvs7cyJszjIywupMCNDDg?e=XCPFjb>`_ which can be used as input to virtual cameras.

Try to create a camera node in your workspace, add a virtual camera that reads the .dcf file
, and run the camera node to display the image in the .dcf file.






