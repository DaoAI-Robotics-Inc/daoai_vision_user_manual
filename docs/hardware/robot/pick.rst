Generic Picking
=============

This is the generic logic of picking process for all kinds of robot. If you want to see Picking of individual robot, you can go to `Different type of Robots <https://daoai-robotics-inc-daoai-vision-user-manual.readthedocs-hosted.com/en/latest/hardware/robot/index.html>`_ to find the specific picking program under the robot page.

You can find the picking program `in here <https://drive.google.com/file/d/1e8qJSOhm25ZiUAlJgulAEamDqmwYkx6s/view?usp=sharing>`_ 

Picking process needs some setup and file beforehand:
	* Calibration result(.yml file): Picking needs the camera to base relation in order to correctly output object locations in scene;
	* Detection Pose: Robot needs a Detection Pose(a waypoint) which is not blocking the camera captures. After each picking cycle, robot moves back here;
	* Place Locations: Robot needs to place the objects after picking them;
	* Gripper grab and loose signal: Robot needs the signal of grabbing objects as well as loosing off the objects;

In pseudo code:

.. code-block:: python

	Picking():
		#Start the communication
		move(detection_pose) # Setup a Detection pose for Picking Process
		if(daoai_find_objects(p1, p2) is objects_found):
			while(daoai_receive_result(p1, p2)):
			move_robot(waypoint_n)
		#Error Handlings
		else if(receive is object_not_found):
			repeat Picking() from beginning
		else if(receive is image_capture_failed):
			repeat Picking() from beginning
		
	end_of_function