Mono 3D
=======

The mono 3d pipeline used mod finder to extract the feature from 2d image, then combining known 3d information for those feature points, finally to detect the object 3d position with a single 2d image.
You could find the detection pipeline from the template workspace "????"

Pipeline Overview
~~~~~~~~~~~~~~~~~
.. image:: Images/mono-3d-det.png
    :width: 80%
    :align: center 

|

As the image above shows, the Mono 3D Detection contains 4 sections in the whole flow:

* Section 1: Load previously defined pose, reader data, calibration context, or to switch between different recipes.
* Section 2: Use the camera to capture 2D data.
* Section 3: First use mod finder 2D mode to find object's anchor feature that will be used as a reference fixture in the second mod finder. Then use mod finder 2D mode to find the object geomatric features in the same 2D image.
* Section 4: Use the Mono 3D node pose estimate mode mapping the trained or set feature to the 2D result from mod finder node into the 3D space.

During the runtime, the execution flow is section 1 -> 2 -> 3 -> 4. And during the defining time, only section 3 in the above image will be used. 

.. image:: Images/mono-3d-det-data.png
    :width: 80%
    :align: center 

|

As the above image shows (TODO, draw professional image), the red line is the data flow for the nodes. And more details can be found with this `workspace <https://domain.invalid/>`_ (TODO, upload a sample workspace for this flowchart, and also upload testing data you can test with). 

Placing the object under the camera
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Place your object under the camera and try to put it as close as possible to the center of your working enviroment (center height of the working cell, and at the center of the image) to capture the sample image while making sure that the object is lying fully in the field of view of the camera. It’s useful to run the camera node continously, and check the **Show Crosshairs** to see the object position

.. image:: Images/mono-3d-teach-model.png
    :width: 62%
    :align: center 

|

Train/Set the Mono model 
~~~~~~~~~~~~~~~~~~~~~~~~
* Method 1 -- Train: We use at least 6 poses to train the Mono Model, the poses can be generated just like Hand-eye calibration. Use the **Manual** flowchart and set the poses like calibration. 
* Or use the chessboard calibration template to generate bag files and read them into the **Mono Train** flowchart.

    .. image:: Images/mono-3d-train.png
        :width: 100%
        :align: center 

|

  * In the **Manage Variables**, set Mod finder mode to 0 or 1 depending on which flowchart is used(detailed in comment).
  
    .. image:: Images/mono-3d-manage-variable.png
        :width: 100%
        :align: center 
        
|

  * If using **Mono Train** flowchart, in the **Constant** node, set integer field to the number of bag files.

    .. image:: Images/mono-3d-constant.png
        :width: 100%
        :align: center 
        
|

  * In the **Mono 3D** node accumulate mode, set the **Calibration Context** to the DA Calibration output file name that exist in the da_calibrations folder in the workspace folder.
    
    .. image:: Images/mono-3d-accumulate.png
        :width: 100%
        :align: center 
        
|

  * In the **Mono 3D** node Final mode, set the output file name. Then proceed to next step.

    .. image:: Images/mono-3d-final.png
        :width: 100%
        :align: center
        
|

  * If using **Manual** flowchart, set the output folder for **Writer** node.

    .. image:: Images/mono-3d-writer.png
        :width: 100%
        :align: center
        
|

* Method 2 -- Set Feature: Instead of training, if the precise relative positions between geo features are known, use the **Mono 3D** node set feature mode. Click **add model**, enter the **Feature Name** corresponding to the geo features' name in **Mod Finder** node(model-n), and enter the xyz relative to the object center(or just make one of the feature to be object center by xyz = [0,0,0]). Make sure each geo feature has it's corresponding set feature. Then set the output file name and run this node only.

.. image:: Images/mono-3d-set-feature.png
    :width: 100%
    :align: center

|

Teach model from camera
~~~~~~~~~~~~~~~~~~~~~~~
Teaching an object model is the most important step when setting up the DaoAI Mod Finder engine to detect your object. The model is the only thing that is used by vision studio to search for your objects in a scene, so a better quality model results in better detections. A high-quality model has the following characteristics:

* It contains as many details of the object as possible,
* It contains only poi  nts that belong to the object itself and
* It exactly matches the side of the object that you want to detect.
  
Continue reading to learn how to build a high-quality model.

Define the anchor feature with the image
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

We use the RGB output from the camera node, and now we run the first mod finder node once to load the image. Then click **add model**, then select a bounding box on the image. It has to be a part of the object that has consistant position relative to itself. To define a good model, see the following sections and the mod finder node introduction (TODO, add the link).

.. image:: Images/mono-3d-define-anchor.png
    :width: 100%
    :align: center 

|

.. tip:: 
    * To define the model more clearly, you could first enlarge the image view in the display.

Define the geo feature with the image
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* After defined the anchor feature, head to the second mod finder node, and run it once to load the image. Now define at least 4 geo features aka four models on the object that has consistant relative position to eachother and the anchor feature defined in previous step. 
  
.. image:: Images/mono-3d-define-geo.png
    :width: 100%
    :align: center 

* After defined the geo features, double click on each of them in the **Models** list, and click the **Define Search Region** button on the bottom left corner. Then select a bounding box for the region of the object where this geo feature at. The search region will be moving with the anchor feature. 

.. image:: Images/mono-3d-search-region.png
    :width: 100%
    :align: center 

* To check search region and anchor feature, simply check the **Show Fixture** option and check geo feature search region(blue box) and anchor feature(yellow box).
  
.. image:: Images/mono-3d-feature-result.png
    :width: 100%
    :align: center

|

Detect the object 
~~~~~~~~~~~~~~~~~
In **Detection** flowchart, click the **Mono 3D** node pose estimate mode, set the **Calibration Context** to DA calibration file name and the Mono 3D file name in **Name this file** section. After everything set, run through the detection flowchart to see if **Mod Finder** nodes displays the correct position of features, and **Mono 3D** pose esitmation pervides same positions as geo features in Mod Finder node.

.. image:: Images/mono-3d-det-setup.png
    :width: 100%
    :align: center

|

.. tip:: 
    * How to define a good anchor feature
        * A good anchor feature must have consistent relative position to the whole object, any shift of the feature will cause inaccuracy. 
        * Make sure the anchor feature is NOT symmetry at all, axial or central.

    * How to define a good geo feature
        * A good geo feature must have consistent relative position to the whole object and other geo features, any shift of the feature will cause inaccuracy. 
        * Make sure the geo feature is NOT symmetry at all, axial or central. Sometimes drawing mask on the feature will prevent symmetry.
        * Define the search region a little bit larger than the geo feature but covering area is not too large.
        * Make sure the reference point is on the object.

    * How to train a good model
        * Make the object close to center of image throughout all capture poses.
        * Make the tilt angle(x,y axis rotation) around 7°, and rotation(around z axis) of ±10° will be enough to train a good model.
