Generic Calibration
===============

This is the generic logic of Calibration for all kinds of robot. 
If you want to see Calibration of individual robot, you can go to Different type of Robots to find the specific Calibration program under the robot page.

The Calibration programs and VMPlayer are `in here <https://drive.google.com/file/d/1e8qJSOhm25ZiUAlJgulAEamDqmwYkx6s/view?usp=sharing>`_.

Calibration process needs some setup beforehand:
	* Calibration Tool: Calibration Chessboard or Calibration Ball installed on robot arm;
	* Calibration Pose: According to different Calibration types, user needs to setup 1 or more waypoints;

In pseudo code:
.. code-block::

	Calibration():
		#Start Communication
		open_socket()

		#Accumulate Poses
		if(vision is in Calibration_mode):
			loop until(No_more_waypoints):
				send(current_pose)
                move_robot(waypoint_n)
			end_of_loop

		#Depending on the type of Calibration, **Vision** or robot will trigger this stop signal
        
		send/receive(done_Calibration_message)
		close_socket()
		end_of_function
