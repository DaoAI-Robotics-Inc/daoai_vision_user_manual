The Vision Interface
=================

The Vision Interface has some variables and functions to communicate between **Vision** and robot. 
This interface should be able to communicate with different type of robots, no matter what language the robot is scrpting in.

These are the examples:

.. toctree::
   :caption: Links below to API usage examples:

   cali
   pick

.. note:: This article assumes an existing implementation of the `socket communication <https://daoai-robotics-inc-daoai-vision-user-manual.readthedocs-hosted.com/en/latest/hardware/robot/socket.html>`_ layer.

Variables
------------------

+-------------------+---------------------------------------------------------------------------------+
| Global Common Variables                                                                             |
+===================+=================================================================================+
| daoai_socket_name | This is the name if socket which is "daoai" at all time.                        |
+-------------------+---------------------------------------------------------------------------------+
| daoai_tcp_pose    | This variable is a vector which contains position and rotation p[0,0,0,0,0,0,0].|
+-------------------+---------------------------------------------------------------------------------+


TCP pose vector contains the positions x, y, z and rotations(different robot uses different length of this vector, for example, **UR** uses 6 of them; **ABB** uses 7 of them). 

+------------------+------------------------------------------------+
| Vision Variable  |                                                |
+==================+================================================+
| daoai_status     | This variable is the command from **Vision**.  |
+------------------+------------------------------------------------+

**daoai_object_type & daoai_remaining_obj & daoai_payload**: These are the 6 payloads of **Vision** replies. ``daoai_object_type`` is referred to ``payload_1`` , ``daoai_remaining_obj`` is ``payload_2`` , ``daoai_payload_x`` are referred payload -> 3, 4, 5, 6.


Robot is able to check this variable after receiving message from **Vision** .
The status essential in communication since it is to determine which process **Vision** is currently in. 
It also represents the result from previous command. For example, if robot is under picking mode, robot requests the objects location, 
**Vision** has different reply based on its detection results: object found, object not found and image capture failure. 
Hence, this status is important to determine the current process between **Vision** and robot.

+------------------------+--------------------------------------------+
| Robot Variable         |                                            |
+========================+============================================+
| payload_1 & payload_2  | These are the payloads of the message.     |
+------------------------+--------------------------------------------+
| daoai_r_command        | This variable is the command from robot.   |
+------------------------+--------------------------------------------+

Robot sends command with/without poses to **Vision** , according to this command, **Vision** is able to determine what is the message and how to process this message. 
This is useful when robot is running on different script with ``Vsion`` flowchart: if robot is trying to perform calibration waypoints, but **Vision** is trying to detect object and perform picking; their commands are 
different in this communication. So that robot is able to detect the pose sent back from **Vision** is in wrong process. This is able to protect unexpected errors and collision. 

For more details about these commands, please see `Socket Communication <https://daoai-robotics-inc-daoai-vision-user-manual.readthedocs-hosted.com/en/latest/hardware/robot/socket.html>`_. 

Functions
------------------

All functions below are request to **Vision**, the communication is one send and one recv.

.. warning:: These are the system functions, do **NOT** directly call thses functions even if you need to modify the script!


.. raw:: html

	<details>
	<summary><a>daoai_open_socket</a></summary>

.. code-block:: text

	Robot opens up the TCP socket via socket settings(port number and IP address).

.. raw:: html
   
	</details>

.. raw:: html

	<details>
	<summary><a>send_robot_data</a></summary>

.. code-block:: text

	Robot sends the current pose and command to Vision.

.. raw:: html
   
	</details>

.. raw:: html

	<details>
	<summary><a>recv_daoai_data</a></summary>

.. code-block:: text

	Robot receives status and corresponding poses from Vision.

.. raw:: html
   
	</details>

.. raw:: html

	<details>
	<summary><a>daoai_close_socket</a></summary>

.. code-block:: text

	Robot closes DaoAI socket and terminates the running program.

.. raw:: html
   
	</details>

|
These are the functions mainly for Manual Calibration process.

.. raw:: html

	<details>
	<summary><a>daoai_start_manual_calibration</a></summary>

.. code-block:: text

	Trigger the vision to start the flowchart of calibration. 
	Robot sends RC_START_MANUAL_CALIBRATION to Vision to request the start of Manual Calibration.

.. raw:: html
   
	</details>

.. raw:: html

	<details>
	<summary><a>daoai_accumulate_calibration</a></summary>

.. code-block:: text

	Accumulate the calibration (will need to send the pose to Vision)
	Until collected all the waypoints, robot calls daoai_stop_manual_calibration()
	to terminate the process.

.. raw:: html
   
	</details>

.. raw:: html

	<details>
	<summary><a>daoai_stop_manual_calibration</a></summary>

.. code-block:: text

	Robot sends RC_STOP_MANUAL_CALIBRATION to Vision to terminating calibration

.. raw:: html
   
	</details>

|
These are the functions mainly for Guidance Calibration process.

.. raw:: html

	<details>
	<summary><a>daoai_accumulate_calibration</a></summary>

.. code-block:: text

	Iccumulate the calibration, and once the vision received enough pose, 
	it will finish the calibraiton automatically

	This is the same function as Manual Calibration

.. raw:: html
   
	</details>

|
These are the functions mainly for Auto Calibration process.

.. raw:: html

	<details>
	<summary><a>daoai_start_auto_calibration</a></summary>

.. code-block:: text

	 This is requesting Vision to start Auto Calibration. Robot sends RC_START_AUTO_CALIBRATION,
	 as well as the current robot pose. Then wait vision to send back acknolegement.

.. raw:: html
   
	</details>

.. raw:: html

	<details>
	<summary><a>daoai_is_calibration_done</a></summary>

.. code-block:: text

	 Wait the response from the Vision, and write the pose into one object, if the return is no, exit

.. raw:: html
   
	</details>

.. raw:: html

	<details>
	<summary><a>daoai_auto_accumulate_calibration</a></summary>

.. code-block:: text

	 Accumulate the calibration (will need to send the pose to vision, and wait vision to send back
	 DAOAI_DONE_AUTO_CALIBRATION)

.. raw:: html
   
	</details>

|
These are the functions mainly for Picking process.

.. raw:: html

	<details>
	<summary><a>daoai_find_objects(payload_1, payload_2)</a></summary>

.. code-block:: text

	 Robot requests Vision to capture image and detect objects in the scene

.. raw:: html
   
	</details>

.. raw:: html

	<details>
	<summary><a>daoai_receive_result</a></summary>

.. code-block:: text

	  Robot waits for Vision side finishing the processing, and write the output to the pick pose

.. raw:: html
   
	</details>

.. raw:: html

	<details>
	<summary><a>daoai_next_object(payload_1, payload_2)</a></summary>

.. code-block:: text

	  Just receiving poses, without capturing new images. This can be applied to 1 capture and pick all 
	  occurences as well. payload_1 is the number of remaining objects in scene.

.. raw:: html
   
	</details>
