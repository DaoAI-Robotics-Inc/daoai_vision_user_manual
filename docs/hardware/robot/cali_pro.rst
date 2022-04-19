Calibration Program
===============

This page is about **Universal Robot** (alias as UR) specific instruction of Calibration. Please make sure you have read `Installation and Setup <https://daoai-robotics-inc-daoai-vision-user-manual.readthedocs-hosted.com/en/latest/hardware/robot/ur_setup.html>`_ and `Calibration <https://daoai-robotics-inc-daoai-vision-user-manual.readthedocs-hosted.com/en/latest/hardware/robot/cali_pro.html>`_.

.. Note ::
	The Calibration programs in default DaoAI package is ready to use. If you do not plan to change the Calibration process flow, we recommend to leave the program as it is. 
	If you decided to modify the program, please make sure it matches the communication protocols with DaoAI Vision side. For detail of communication details please see `Socket <https://daoai-robotics-inc-daoai-vision-user-manual.readthedocs-hosted.com/en/latest/hardware/robot/socket.html>`_ and `Communication Flow <https://daoai-robotics-inc-daoai-vision-user-manual.readthedocs-hosted.com/en/latest/hardware/robot/comm.html>`_ .

The goal of Calibration is to confirm the relation between Robot Base and Camera(Camera to Base).

.. image:: Images/calibration_goal.png
    :align: center
    
|

Different Calibration Programs
-----------------------

Manual Calibration
**********************

First of all, we opens up the Manual_Calibration.urp, connect robot with **Vision**.

.. image:: Images/load_cali_pro.png
    :align: center
    
|

.. image:: Images/man_cali_pro.png
    :align: center
    
|

The program flow would looks like this:

.. image:: Images/man_cali_snap_1.png
    :align: center

.. image:: Images/man_cali_snap_2.png
    :align: center
    
|

In this Manual Calibration sample program, robot opens socket connecting to **Vision**, traverse all the waypoints, then ends Calibration process and close the socket. In pseudo code:

.. code-block:: python

   Manual Calibration():
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


Auto Calibration
**********************
Opening up the Auto_Calibration.urp, connect robot with **Vision**.

.. image:: Images/auto_cali_flows.png
    :align: center
    
|

.. image:: Images/setup_auto_cali.png
    :align: center
    
|

The program flow would looks like this:

.. image:: Images/auto_pro.png
    :align: center
    
|

In this Auto Calibration sample program, robot opens socket connecting to **Vision**, sending message to **Vision** to confirm Auto Calibration process. 

Repeat: UR sends the current pose to **Vision**; **Vision** accumulates the pose then calculates and replies back the next pose to UR; then UR moves to next pose; 

Until **Vision** has collected enough poses, it sends a stop signal to UR terminating the Auto Calibration process. UR closes the socket. 
In pseudo code:

.. code-block:: python
	Auto_Calibration():
		daoai_start_auto_calibration()
		Loop daoai_auto_accumulate_calibration():
			robot_move(receive_pose)
		end_of_loop

	end_of_function


The Waypoints
-----------------------

Waypoints are important for the Calibration output. If the waypoints are not good, the Calibration output would have large error. Which would affect the detection pose results and robot might not be able to pick.

Waypoint locations should try to follow the clockwise or counter-clockwise direction within camera scene. The first waypoint can be at the middle(Or anywhere you could remember). Then central top, central top to the right......until the wapoint can form a circle to produce enough poses.
Each waypoints should have slightly tilt and rotation. Try to keep tilting degree small, and rotate around the wrists.


.. warning ::
	Guidance Calibration and Auto Calibration only needs to setup the first waypoint. For Guidance Calibration and Auto Calibration, first wapoint should always be the central location.

.. image:: Images/cali_centre_waypoint.png
    :align: center
    
This is the sample central waypoint. 

|
.. image:: Images/cali_waypoint_layout.png
    :align: center

This is the sample waypoints layout poses, this is 9 waypoints. If you decided to add more waypoints to minimize the error, you would need to modify the program. 
But the basic concept of wayppoints is the same: waypoints can form a circle around the central waypoint.

Execute the Program
-----------------------

Click ``Run`` on both **Vision** and UR, now you should see the robot moves to different poses, Camera captures and **Vision** accumulates the data. You just need to sit back and relax, wait for it to be done!

.. warning ::
	Even though you can sit back and relax, but remember to MONITOR the robot movement!!! Do NOT hit anything!!!
