3D Picking 
===========

3D Picking is the most common way of picking. It involves robot arm gripping, sucking and magnetic picking etc. 
The main difference between 2D & 3D picking here is due to camera limitation. 
Some cameras are able to capture 3D images but some are not. 
The camera hardware limitation will be the constraint to our actual picking procedure. 

TODO -> Image

For 3D picking, the previous detection procedure will detect the object positions in the point cloud coordinate, 
and the calibration procedure will detect the robot and camera relationship. 
The picking step is mapping what the camera detected to where to pick with the robot end effector. 

.. tip:: The camera and point cloud coordinate has a 180 degree rotation on the rx axis. 

.. toctree::
    :hidden:
    
    tcp
    pick-point
    pick-strategy
    collision-p


