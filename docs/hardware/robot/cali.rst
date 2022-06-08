Calibration Program
===============

This is the generic logic of Calibration for all kinds of robot. 
If you want to see Calibration of individual robot, you can go to Different type of Robots to find the specific Calibration program under the robot page.

.. warning::
	You must make sure the `Euler Angle Order <>`_ is matching before you working on Calibration. TODO

The Calibration programs and VMPlayer are `in here <https://drive.google.com/file/d/1e8qJSOhm25ZiUAlJgulAEamDqmwYkx6s/view?usp=sharing>`_. 
Details for UR Calibration program is in `here <https://daoai-robotics-inc-daoai-vision-user-manual.readthedocs-hosted.com/en/latest/hardware/robot/cali_pro.html>`_.

Calibration process needs some setup beforehand:
	* Calibration Tool: Calibration Chessboard or Calibration Ball installed on robot arm;
	* Calibration Pose: According to different Calibration types, you would need to setup 1 or more waypoints;

In pseudo code:

.. code-block::

	Calibration():
		#Start Communication
		daoai_start_manual_calibration() #Opens socket, sends start signal to Vision

		#Accumulate Poses
		if(vision is in Calibration_mode):
			loop daoai_manual_accumulate_calibration():
				move_robot(waypoint_n)
			end_of_loop

		#Depending on the type of Calibration, **Vision** or robot will trigger this stop signal
        
		daoai_stop_manual_calibration() # Close socket and halt robot program
		end_of_function
