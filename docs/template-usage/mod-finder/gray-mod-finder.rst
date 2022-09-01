RGB Mod Finder
===================

Pipeline Overview
~~~~~~~~~~~~~~~~~~~~~~~~

.. image:: images/flow.png
    :align: center

|

For general picking pipelines, camera & robot work together to **see** and **pick**. **Vision** is a software layer to communicate between all these hardwares. 
The stages above are essential for all the required relations in this calculation. Therefore, even if the requirements are different from project to project, the core 
calculation is similar. 

The RGB Mod Finder pipeline has 4 stages: 

    #. **Teach Pose**: Teach/demonstrate the picking pose to robot;

    #. **Detection**: Detect the object location in scene;

    #. **Pose Transformation** (Picking flowchart): Transform all the poses and relations for picking procedure;

    #. **Picking**: Robot communication and actual picking;


Teach Pose
~~~~~~~~~~~~

Teach Pose is a stage for you to show the robot: how to pick the object. It has 2 kinds of teach pose, mainly differ from whether or not the robot is involved. For **Mod Finder** templates, 
we use the teach pose which the robot is involved. 

.. image:: images/teach_pose.png
    :align: center

|

The image shown above is the example of typical teach pose procedures. It is essential for robot to know how to approach its gripper to object. 
This stage is required which it calculates the **Object in Tool** relation.

You can split this pipeline into 5 major parts:

1. **Calibration** node, load in the calibration result from local ``.yml`` file. You can checkout these articles for `Calibration node <https://daoai-robotics-inc-daoai-vision-user-manual.readthedocs-hosted.com/en/latest/nodes/Calibration/calibration.html>`_ and `Sphere Calibration node <https://daoai-robotics-inc-daoai-vision-user-manual.readthedocs-hosted.com/en/latest/nodes/Calibration/sphere_calibration.html>`_. And details of calibration procedures are :ref:`Board Calibration` and :ref:`Sphere Calibration`. 

2. **Detection** flowchart is executed here to find out the current **Object in Cloud** relation. When you execute this flowchart for the first time, you will need to define the model. You can check `DA Alignment section <https://daoai-robotics-inc-daoai-vision-user-manual.readthedocs-hosted.com/en/latest/nodes/DA%20Modules/DA%20Alignment%20Node.html>`_ for instructions of defining the model. 

3. **Robot Read** node is reading in the robot current pose, **Tool in Base** relation. 

4. **Transformation Tree** node collects all the relations and generate the **Tool in Object** pose for **Gripper** node. 

Detection
~~~~~~~~~~~~~~~~~~

.. image:: images/gray_mod_finder_det.png
    :align: center 

|

As the image above shows, the RGB Mod Finder contains 5 sections in the whole flow:

* Section 1: Used the camera to capture 3D data, then use cloud process (adjust bounding box feature) to set the working cell of the project.
* Section 2: Used mod finder 2D mode to find the object in the 2D image.
* Section 3: Use the reconstruct node projecting feature to map the 2D result from mod finder node into the 3D space.
* Section 4: Perform the inverse operation on the model cloud in order to align the model cloud with scene cloud.
* Section 5: The alignment in this section was used to align the 3D model from section 4 into the 3D space. It takes in the output from section 3, where the reconstruct node output the initial pose of the object. You will also need to define the model before executing this node. `Checkout this article about how to define models for DA Alignment <https://daoai-robotics-inc-daoai-vision-user-manual.readthedocs-hosted.com/zh_CN/latest/nodes/DA%20Modules/DA%20Alignment%20Node.html>`_.

During the runtime, the execution flow is section 1 -> 2 -> 3 -> 5. And during the defining time, the execution flow is section 1 ->2 -> 3 -> 4 -> 5. After defining the model, as long as you do not redefine the model again, **DA Alignment** node will not update the pose from **Section 4**. Therefore, when performing picking procedure, you do not need to worry about **Section 4**.

.. tip:: You can also learn about the main ideas behind the RGB mod finder engine by watching this video tutorial. (TODO, record a video)

Teach model from camera
~~~~~~~~~~~~

Teaching an object model is important step when setting up the DaoAI Mod Finder engine to detect objects. 
Mod Finder needs a good model to identify objects in scene. Mod Finder uses RGB or Depth image to detect objects, therefore anything captured in camera could be possibly the object. 
How can Vision recognizes these objects? By comparing from the model and the image. Hence, good model plays the essential role in this process.
  
The rest of this article is about how to define model. If you want to know what is good model, please see :ref:`Define Models`.


Placing the object under the camera
~~~~~~~~~~~~~~

Place your object under the camera and try to put it as close as possible to the center of your working environment (center height of the working cell, and at the center of the image) to capture the sample image while making sure that the object is lying fully in the field of view of the camera. It’s useful to run the camera node continuously, and turn on the point cloud view to see the image quality of the object. 

.. image:: images/teach-model-picture_gray_mod_finder.png
    :align: center 

|

Isolating the object 
~~~~~~~~~~~~~~
Usually the camera field of view will be larger than the region of interest, thus the first step usually is to setup the boundary for the useful information. 
You could run the cloud process node, and make sure the **Adjust Bounding Box** options was on in the cloud process display setting. 
Then execute the Cloud Process node. Then you could adjust the bounding box. 

.. image:: images/roi.png
    :align: center 

.. tip:: When adjust the bounding box, you could press **R** to reset to the original view, For more information of Adjusting Box. checkout this `article <https://daoai-robotics-inc-daoai-vision-user-manual.readthedocs-hosted.com/en/latest/faq-trouble-shooting/adjust_box/index.html>`_.

Define the 2D Model with the Image
~~~~~~~~~~~~~~~

We use the RGB output from the cloud process node, and now we run the Mod Finder node once to load in the image. 
Then click **add model**, then select a bounding box on the image. 
To define a model, click the ``+`` sign. 

.. image:: images/plus_sign.png
    :align: center 

|

Then defining the model in scene.

.. image:: images/model_def.png
    :align: center 

|

You can checkout :ref:`Define Models` to see how to define a good model for Mod Finder node. 

Poses Generation & Transformation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. image:: images/pose_tran.png
    :align: center 

|

These 3 nodes in Detection flowchart will generate the poses output the **Object in Cloud** relation for further calculations. 
We will skip this part here, and you can checkout the articles for `Reconstruct node <https://daoai-robotics-inc-daoai-vision-user-manual.readthedocs-hosted.com/en/latest/nodes/3D%20Processing/reconstruct.html>`_ 
and `DA Alignment node <https://daoai-robotics-inc-daoai-vision-user-manual.readthedocs-hosted.com/en/latest/nodes/DA%20Modules/DA%20Alignment%20Node.html>`_. Which **DA Alignment** node section will cover the pose transformation detail. 

.. image:: images/picking.png
    :align: center 

After the Detection pipeline, you have the objects locations in scene. Then, these poses will need transformations, since the robot requires the **Tool in Base** relation for 
all the objects. As the image shown above, our template will process the collision avoidance for these objects in scene. Then providing the orders for these objects, and send it 
to robot.

You can checkout details about `Gripper node <>`_, `Collision Avoidance node <>`_ and `Pick Sort node <>`_.

After these transformations, robot will receive a pose regarding to its **Tool in Base** relation to perform picking.