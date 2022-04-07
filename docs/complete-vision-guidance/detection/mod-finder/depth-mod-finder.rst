Depth Mod Finder 
===============

The Depth Mod Finder pipeline has 3 stages, one is to find the object on depth image, then map to 3D space, and finally use alignment to get accurate result.

Pipeline Overview
~~~~~~~~~
.. image:: Images/depth_mod_finder_det.png
    :width: 40%
    :align: center 
As the image above shows, the Gray Mod Finder contains 5 sections in the whole flow:

* Section 1: Used the camera to capture 3D data.
* Section 2: This section was used to crop the 3D model of the object, and use it for the alignment. And this section will only be executed once during the defining time.
* Section 3: Use cloud process (adjust bounding box feature) to set the working cell of the project. 
* Section 4: Mod Finder node is used in model define stage as well as detection stage.
* Section 5: The alignment in this section was used to align the 3D model from section 2 into the 3D space. It takes in the output from section 2 or section 3, where the Mod Finder node output the initial pose of the object.

.. image:: Images/var_change.PNG
    :width: 40%
    :align: center  

During the runtime, the execution flow is section 1 -> 3 -> 2 -> 4 -> 3 -> 4 -> 5. When defining model, set ``detection.detection_status`` to ``0`` which would reset to setup working cell stage. 
Then it enters stage 2 defining model. Afterwards, it statys on stage 3 detection mode until user changes variable to reset the stage.

.. image:: Images/depth_modfinder_temp.png
    :width: 40%
    :align: center 

As the above image shows, the red, green and blue arrow is the data flow for the nodes. 
Green arrow is the detection flow of the flowchart; Red arrow is the flow for defining model in scene; Blue arrow is to define the working cell in image.
And more details can be found with this `workspace <https://drive.google.com/uc?export=download&id=171FzY6Br1Uv6vjGTCblTZD6l76cuyRWh>`_ 

.. tip:: You can also learn about the main ideas behind the depth mod finder engine by watching this video tutorial. (TODO, record a video)

Teach model from camera
~~~~~~~~~~~~

Teaching an object model is important step when setting up the DaoAI Mod Finder engine to detect your object. 
The model is the reference for Vision studio to search for your objects in a scene, so a better quality model results in better detections. 
A high-quality camera model has the following characteristics:

* It contains as many details of the object as possible,
* It contains only points that belong to the object itself and
* It exactly matches the side of the object that you want to detect.
  
Continue reading to learn how to build a high-quality model.


Placing the object under the camera
~~~~~~~~~~~~~~

Place your object under the camera and try to put it as close as possible to the center of your working enviroment (center height of the working cell, and at the center of the image) to capture the sample image while making sure that the object is lying fully in the field of view of the camera. It’s useful to run the camera node continously, and turn on the point cloud view to see the image quality of the object. 

.. image:: Images/teach-model-picture_gray_mod_finder.png
    :align: center 

|

Isolating the object 
~~~~~~~~~~~~~~
Usually the camera field of view will be larger than the region of interest, thus the first step usually is to setup the boundary for the useful information. 
You could run to the **Section 3** Cloud Process node, and make sure the **Adjust Bounding Box** options was on in the cloud process display setting. 
Then execute the Cloud Process node. Then you could adjust the bounding box. 

.. image:: Images/roi.PNG
    :align: center 

.. tip:: When adjust the bounding box, you could press **R** to reset to the original view, and blabla for the operation trick

Define the Model with the Image
~~~~~~~~~~~~~~~
.. note:: 
    Defening a model from scene requires the flowchart in defining mode. Constant node should be set to ``true`` in order to switch to defining mode. ``false`` represents flowchart is in detection mode.

We use the depth output from the DA CloudNDepth Conv node, and now we run the Mod Finder node once to load in the image. 
Then click **add model**, then select a bounding box on the image. 
To define a model, click the ``+`` sign. 

.. image:: Images/plus_sign_depth.PNG
    :align: center 

|

Then defining the model in scene.

.. image:: Images/model_def_depth.png
    :align: center 

|

How to set good model matching parameters
~~~~~~~~~~~~~~~~~~~~

Double clicking on the model brings up the model parameter configuration.

.. image:: Images/model_param_dep.PNG
    :align: center 

These parameters are important for detection such that:

* **Acceptance** is the object acceptance in scene. Since Gray Mod Finder uses gray image to detect objects, some pixels of same color in image might form a similar shape as model. Hence, increasing the acceptance higher to ensure it detects the objects and objects only. But if the acceptance is too high, Vision would try to look for objects which has identical pixels with model. This is not so true in real life enviornment since objects might be in different place, when camera captures, the shape of object would slightly change due to angle changes or lighting changes.

.. image:: Images/acc_high.PNG
    :align: center 

When setting acceptance too high, detected 1 occurence of objects but there are 8

.. image:: Images/acc_low.PNG
    :align: center 

When setting acceptance too low, detected 32 occurence of objects but there are 8

* **Reference Point** is the point which Vision detects and perform picking. Reconstruct node generates the object coordinates based on this reference point. Hence, this point would affect the height of object when picking(you do NOT want the gripper to penetrate though the object). This green cross is the reference point:

.. image:: Images/ref_point_dep.PNG
    :align: center 

* **Mask** can cover the area which we do not want to include in model. As we opens up the model parameter configuration, we can see the red lines on the object. These red lines are the shape which is the shape Vision uses for detecting objects. 

.. image:: Images/model_param.PNG
    :align: center 

As the image shown, the label in the middle is included as the shape of object now. We do not want this label since the other side of this object does not have label!
We can click ``Draw Mask`` to apply mask on the model:

.. image:: Images/draw_mask_model_dep.PNG
    :align: center 

So that we can erase all the non-interested details of the model.

.. image:: Images/good_model_dep.PNG
    :align: center 

|

After define the model, head to the DA Alignment node, and run it. You will see model cloud aligns with the object positions. 

.. image:: Images/da_align.PNG
    :align: center 

.. tip:: * To define the model more clearly, you could first enlarge the image view in the display.

.. image:: Images/model_cloud.PNG
    :align: center

After that, executing flowchart to **Section 2**, Cloud Process node crops the defined model and Writer saves the model cloud to local directory. 

.. warning:: 
    The object we crop in Cloud Process node **MUST** be the same object we defined eariler in Mod Finder node. 
    In this case, we used bottom right corner object to define model in Mod Finder; then we have to crop the same object for moel cloud.
    If model is not the same object as the cloud, DA Alignment node would not be able to align the model cloud with objects.

.. image:: Images/align_wrong.PNG
    :align: center 

This is the result of alignment when using different object cloud.

The reason behind this result is that DA Alignment takes the model cloud as well as the initial pose of this object from Mod Finder. Reconstruct node process the objects from Mod Finder, 
it generates the pose(coordinates) for the objects. Then Pose Operation node inverse the pose, since the output from Reconstruct is Object-in-Cloud relation, DA Alignment needs Cloud-in-Object relation to align model cloud with object pose. Hence, if the cloud is not the same with model, alignment result is not the correct relations.

How to teach a good model
~~~~~~~~~~

As mentioned earlier, teaching a good model would have great benefitial to detection result. What is good model? 

Good model should be:
    * Model has clear object outline and good object point cloud. A good point cloud should only have tiny area of overexposed pixels or even better that does not have any overexpsed pixels. 
    * Model contains the object and object itself only. The surface should not be included in the model when cropping for Cloud Process.
    * Model Acceptance should be low enough to detect all the occurences of objects **AND** as high as possible to detect all the occurences of the object.

.. tip:: How to adjust this Acceptance level? Set this acceptance level to able to detect all occurences of object; then slowly increases the acceptance level until detected occurences less than what it suppose to be(For example, 8 objects in scene, and we keep increasing the acceptance level until detected occurences is 7 or less). Then decreasing it back to the highest accetpance level which is able to detect all ocurences.




