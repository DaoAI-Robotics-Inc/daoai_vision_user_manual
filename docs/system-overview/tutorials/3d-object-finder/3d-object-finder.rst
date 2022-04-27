3D Object Finder 
----------------
Objective
~~~~~~~~~
This tutorial is to guide you to use the 3d object finder node to locate the object using the features of the cloud. 

Steps
~~~~~~
1. :ref:`Create a new workspace`
2. :ref:`Connect the camera to the Vision software`
3. :ref:`Insert the nodes`
4. :ref:`Configure the link expression inside each node`
5. :ref:`Workspace Data & Video Recordings`

Create a new workspace
~~~~~~~~~~~~~~~~~~~~~~~

Please use the link to checkout the details of `Link <https://daoai-robotics-inc-daoai-vision-user-manual.readthedocs-hosted.com/en/latest/system-overview/tutorials/new-workspace/new-workspace.html>`_.

Connect the camera to the Vision software
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Please use the link to checkout the details of `Link <https://daoai-robotics-inc-daoai-vision-user-manual.readthedocs-hosted.com/en/latest/system-overview/tutorials/new-workspace/new-workspace.html>`_.

Insert the nodes
~~~~~~~~~~~~~~~~~

In general, we use the 3D Object Finder node to identify the object inside the 3D scene cloud; therefore, the basic setup is to use the camera point cloud as the input of the 3D Object Finder. To make sure the object can be perfectly mapped in the scene, the Alignment node is added under to 3D Object Finder node to improve the accuracy.

.. image:: Images/1.png
    :width: 100%
    :align: center
|

Configure the link expression inside each node
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The first step the operator needs to do is to select the search type

.. image:: Images/2.png
    :width: 100%
    :align: center
|

By selecting normal, the node's point cloud will consist of planes or curved surfaces.

.. image:: Images/3.png
    :width: 100%
    :align: center
|

If the operator selects edge, the node will create the point cloud using the feature points along the object's edge.

.. image:: Images/4.png
    :width: 100%
    :align: center
|

Once the operator finishes defining the type, the remaining sections of the dialogue can be visualized.
   
.. image:: Images/5.png
    :width: 100%
    :align: center
|

If the operator selects normal, the operator should click the blue button to the right of the Scene Cloud node to open the Expression Link Dialog and insert the scene cloud's link.

.. Attention::
   While the camera node is used as the scene cloud's input in the example above, other nodes such as reader and cloud process can also be used as the scene cloud's input.

The result displayed in the View interface varies according to the search type selected by the operator at the start.
The operator can add and define an object's model in the Models section by pressing the "+" button. In the section, a "model x" will be displayed to inform the operator that the model was successfully created.

.. image:: Images/6.png
    :width: 100%
    :align: center
|

By double-clicking on model 1, the ObjFinder3DModelConfig dialogue for editing the model's parameters will open. The operator can either load the model mesh from the device or define the object from the scene cloud within Model Type.

.. image:: Images/7.png
    :width: 100%
    :align: center
|

By choosing the type as mesh, the program will ask the operator to add the mesh path. 


.. image:: Images/8.png
    :width: 100%
    :align: center
|
.. image:: Images/17.png
    :width: 100%
    :align: center
|

.. Attention::
   Normally the model type loaded into the path should be ply.

However, if the operator chooses to load the model from the scene, then the program will ask the operator to define the Model from the scene cloud.

.. image:: Images/9.png
    :width: 100%
    :align: center
|
.. image:: Images/10.png
    :width: 100%
    :align: center
|
.. image:: Images/11.png
    :width: 100%
    :align: center
|

The operator can use this function in the Model Parameters node to enhance the quality of the point cloud by editing the Feature Detail and Downsample Strength. By clicking the Update Model button, the operator can update the editing information.

.. image:: Images/12.png
    :width: 100%
    :align: center
|
.. image:: Images/13.png
    :width: 100%
    :align: center
|

Both features have 3 options to choose: 

The Feature Detail property specifies how many model features are used in the calculation. The higher the value, the more features are calculated. Downsampling determines the object's point cloud's quality. A lower value indicates a denser point cloud was used in the subsequent calculation.

.. image:: Images/14.png
    :width: 100%
    :align: center
|

The Pose Constraints dialog can be used to help the operator to define objects more accurately. 

After defining the model, the operator can close the ObjFinder3DModelConfig Diglog and edit the parameters inside the Finder Settings. 

.. image:: Images/15.png
    :width: 100%
    :align: center
|

The operator should enter the desired number of detected objects in the Number of Occurrences field and adjust the Acceptance Threshold to ensure that no additional or fewer objects are displayed in the scene.

.. image:: Images/16.png
    :width: 100%
    :align: center
|

The operator can use the Alignment node to perform a second alignment between the detected poses and the scene to increase the accuracy.

Workspace Data & Video Recordings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The used data for this demo, and the video recording for this demo was stored online with this:

`3D_Object_Finder <https://daoairoboticsinc-my.sharepoint.com/:f:/g/personal/wzhao_daoai_com/ElfERbA6veVMhl0YbWQOWR4B5nVnXy_vmYAPLFfLXSfawA?e=fGXkUX>`_