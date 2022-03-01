Configure Working Platform
***********************************

Cameras are used to provide information about the working environment, such as images and point clouds. The workspace must be connected to cameras (real or virtual)
in order to capture such input data.

Also, in order to pick up the objects, the workspace must be connected to robots.

Vision software provides detection, connection management and configuration of cameras and robots. They are located under platform config menu.

In the template workspace, the camera and robot are already configured, but not connected (virtual camera that uses local files as captured result and virtual robot that uses UR robot server).
You can just connect them in the platform config page.

.. toctree::
   :maxdepth: 2
    
   Platform

Refer to `Hardware requiements` on details regarding using cameras and robots together with vision software.