The Vision Interface
=================

The Vision Interface has some variables and functions to communicate between ``Vision`` and robot. 
This interface should be able to communicate with different type of robots, no matter what language the robot is scrpting in.

These are the examples:

.. toctree::
   :caption: Type of Interface

   pick
   cali

Variables
------------------

daoai_status
~~~~~~~~~
This variable is the command from ``Vision`` . Robot is able to check this variable after receiving message from ``Vision`` .
The status essential in communication since it is to determine which process ``Vision`` is currently in. 
It also represents the result from previous command. For example, if robot is under picking mode, robot requests the objects location, 
``Vision`` has different reply based on its detection results: object found, object not found and image capture failure. 
Hence, this status is important to determine the current process between ``Vision`` and robot.

daoai_r_command
~~~~~~~~~~~
This variable is the command from robot. Robot sends command with/without poses to ``Vision`` , according to this command, ``Vision`` is able to determine what is the message and how to process this message. 
This is useful when robot is running on different script with ``Vsion`` flowchart: if robot is trying to perform calibration waypoints, but ``Vision`` is trying to detect object and perform picking; their commands are 
different in this communication. So that robot is able to detect the pose sent back from ``Vision`` is in wrong process. This is able to protect unexpected errors and collision. 

For more details about these commands, please see *Link . 

Functions
-------------

Calibration
~~~~~~~~~

Manual Calibration
***************

.. raw:: html

	<details>
	<summary><a>daoai_start_manual_calibration()</a></summary>

.. code-block:: text

	Trigger the vision to start the flowchart of calibration. 
	Robot sends RC_START_MANUAL_CALIBRATION to Vision to request the start of Manual Calibration.

.. raw:: html
   
	</details>

.. raw:: html

	<details>
	<summary><a>daoai_accumulate_calibration()</a></summary>

.. code-block:: text

	Accumulate the calibration (will need to send the pose to Vision)
	Until collected all the waypoints, robot calls daoai_stop_manual_calibration()
	to terminate the process.

.. raw:: html
   
	</details>

.. raw:: html

	<details>
	<summary><a>daoai_stop_manual_calibration() </a></summary>

.. code-block:: text

	Robot sends RC_STOP_MANUAL_CALIBRATION to Vision to terminating calibration

.. raw:: html
   
	</details>


|

Guidance Calibration
***************

.. raw:: html

	<details>
	<summary><a>daoai_accumulate_calibration()</a></summary>

.. code-block:: text

	Iccumulate the calibration, and once the vision received enough pose, 
	it will finish the calibraiton automatically

	This is the same function as Manual Calibration

.. raw:: html
   
	</details>

|

Auto Calibration
*************

.. raw:: html

	<details>
	<summary><a>daoai_send_current_pose()</a></summary>

.. code-block:: text

	Sends RC_DAOAI_NO_COMMAND, and sends the pose to Vision

.. raw:: html
   
	</details>

.. raw:: html

	<details>
	<summary><a>daoai_start_auto_calibration()</a></summary>

.. code-block:: text

	 This is requesting Vision to start Auto Calibration. Robot sends RC_START_AUTO_CALIBRATION,
	 and wait vision to send back acknolegement


.. raw:: html
   
	</details>

.. raw:: html

	<details>
	<summary><a>daoai_is_calibration_done()</a></summary>

.. code-block:: text

	 Wait the response from the Vision, and write the pose into one object, if the return is no, exit

.. raw:: html
   
	</details>

.. raw:: html

	<details>
	<summary><a>daoai_accumulate_calibration()</a></summary>

.. code-block:: text

	 Accumulate the calibration (will need to send the pose to vision, and wait vision to send back
	 DAOAI_DONE_TASK)

.. raw:: html
   
	</details>
|

Picking
~~~~~~~~~

.. raw:: html

	<details>
	<summary><a>daoai_find_objects(payload_1, payload_2)</a></summary>

.. code-block:: text

	 Robot requests Vision to capture image and detect objects in the scene

.. raw:: html
   
	</details>

.. raw:: html

	<details>
	<summary><a>daoai_receive_result()</a></summary>

.. code-block:: text

	  Robot waits for Vision side finishing the processing, and write the output to the pick pose

.. raw:: html
   
	</details>

.. raw:: html

	<details>
	<summary><a>daoai_next_object(payload_1, payload_2)</a></summary>

.. code-block:: text

	  Just receiving poses, without capturing new images. This is mostly for 1 capture and pick all 
	  occurences

.. raw:: html
   
	</details>






