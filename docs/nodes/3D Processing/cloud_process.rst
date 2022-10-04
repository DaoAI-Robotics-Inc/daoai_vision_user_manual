Cloud Process Node
===================

Overview 
--------

Cloud process node is a utility node that performs arbitrary number of operations on the input point cloud and outputs the processed point cloud.

.. image:: Images/cloud_process/cloud_process.png
   :align: center

Input & Output
--------------

+----------------------------------------+-------------------------------+----------------------------------------------------+
| Input                                  | Type                          | Description                                        |
+========================================+===============================+====================================================+
| Point Cloud                            | pointCloud                    | The input pointCloud to be processed by the node.  |
+----------------------------------------+-------------------------------+----------------------------------------------------+

+-------------------------+-------------------+---------------------------------------------------------------------------------------+
| Output                  | Type              | Description                                                                           |
+=========================+===================+=======================================================================================+
| outputCloud             | pointCloud        | The output point cloud after processing.                                              |
+-------------------------+-------------------+---------------------------------------------------------------------------------------+
| image                   | Image             | The rgb image of the processed point cloud.                                           |
+-------------------------+-------------------+---------------------------------------------------------------------------------------+
| depthMap                | Image             | The depth image of the processed point cloud.                                         |
+-------------------------+-------------------+---------------------------------------------------------------------------------------+
| referenceFrame          | Pose              | The reference coordinate defined in 3d process node, used as input of other nodes.    |
+-------------------------+-------------------+---------------------------------------------------------------------------------------+
| mergePoses              | Vec<3DPoses>      | Transformation applied to the second point cloud when merging two point cloud.        |
+-------------------------+-------------------+---------------------------------------------------------------------------------------+

Node Settings
-------------

.. image:: Images/cloud_process/settings.png
   :align: center

- **Enable RGB Restore Mode** (Default: checked): 
   Sometimes during the cloud process the rgb information of some points inside the region of interest are lost, because the corresponding clouds are noise.
   This mode restores some of the rgb information using the average of neighboring points.

- **Mode** (Default: Box):
   Box mode, where the rgb is the average of points in a square kernel; or Tight mode, where the rgb is the average of neighboring valid points.

- **Iteration** (Default: 4, Range: [1-100]): 
   Number of times the rgb restore operation is applied.

- **Erosion Size** (Default: 3, Range: [1-10]): 
   Size of erosion kernel, bigger the number, more rgb information maybe restored.

- **Dilation Size** (Default: 3, Range: [1-10]): 
   Size of dilation kernel, bigger the number, more rgb information maybe restored.

- **Advanced** (Default: unchecked):
   When checked, show available advanced settings in operation parameters.

Operations and Parameters
-------------------------

This node supports a variety of operations. Each of them has unique parameters.

Downsample
~~~~~~~~~~

This operation takes in 3 spatial resolutions (x, y, z) which are used to define a voxel grid size from which to subsample the points. 
The output of this operation will be a new cloud that is subsampled to contain fewer points than the original. 
Note this **does not maintain the organized structure of the output cloud** (output only contains a height of 1).

.. image:: Images/cloud_process/cloud_process_downsample.png
   :align: center

Outlier Removal
~~~~~~~~~~~~~~~

This operation is similar to downsample. It reduces the number of points in the cloud; however, it uses the mean and variance of the distance between points. 
Based on the input values (k and cutoff) it calculates the mean and variance in the distance of the given point from its K immediate neighbors. 
For all points whose mean distances are outside an interval defined by the global distances mean and standard deviation can be considered as outliers and trimmed from the dataset. 
Specifically, we calculate the following to determine if the point is an outlier or not. 

.. image:: Images/cloud_process/outlier-removal-eq.png
   :align: center

.. image:: Images/cloud_process/cloud_process_outlier_removal.png
   :align: center

Crop a Region
~~~~~~~~~~~~~

This operation takes in a field name (“x” “y“ or “z”) and the bounds for that region. The output of this operation will return a cloud with that specific region cropped.

.. image:: Images/cloud_process/cloud_process_crop.png
   :align: center

Normals
~~~~~~~

With the Normals operation, we estimate the surface normal of each region in the point cloud. 
The operation takes in three values(depth factor, normal smoothness, and k neighbors). 
Most of the time there is no need to modify any of the default values. This operation has no visual effect.

* Normal Depth Factor: The depth change threshold for computing object borders
* Normal Smoothness: The factor which influences the size of the area used to smooth normals
* Normal K Neighbors: This input is **only required if the input cloud is unorganized** and, combined with the normal smoothness value, defines the search region.

 The computed normal data will be stored with the point cloud object. 

Transform Coordinates
~~~~~~~~~~~~~~~~~~~~~

This applies a 3D affine transform to the input point cloud and returns the transformed version of the cloud.

.. image:: Images/cloud_process/cloud_process_transform.png
   :align: center

Dynamic Box Filter
~~~~~~~~~~~~~~~~~~

This operation crops the z region of the cloud by finding the point that is highest and cropping everything below a certain threshold. 
This operation is usually used when the users want to keep point cloud within a certain range in depth (e.g. the top layer of a pile of boxes).

Please note that this filter is based on the reference coordinate defined in the previous operation. Before using this operation, use set reference frame 
operation to set the reference coordinate.

The filtering process starts from the origin of the reference coordinate. It divides point cloud into partitions along z- direction. The starting partition 
is the first partition with points more than *Points Threshold* (user-defined parameter). Then the filter will keep points withing the following *Distance Threshold* mm.

.. image:: Images/cloud_process/cloud_process_dynamic_box.png
   :align: center

* Threshold: range in millimeter along z axis, the points in range will be kept
* Points Threshold: number of points a segmentation along z axis must have to be considered a staring point of filtering, this determines the top of the dynamic box.

Adjust Bounding Box
~~~~~~~~~~~~~~~~~~~

.. image:: Images/cloud_process/cloud_process_adjust_box.png
   :align: center
|

This operation crops the cloud by placing a bounding box that the you can adjust by clicking on the adjust box option. 
Once the you set the bounding box the first time it will remember this choice so that you do not have to reconfigure the box again. 
You can uncheck the Adjust box option so that they do not have to interact with the box once the adjustments are finished.

To enable the Adjust Bounding Box function, make sure to check the Adjust Box before running. 

When the Adjust Box is checked, a bounding box will display in the scene every time the Cloud Process Node is being run. To adjust the bounding box:

* Mouse left key on the box surface to rotate the box
* Mouse right(press down) key on the box to move around the whole box
* Mouse left key outside the box to rotate the scene
* Mouse left(press down) key outside the box to move the whole scene
* Mouse mid(roll) key to zoom in/out the scene
* Drag on the sliding box to adjust box's rotation around x,y,z axis
* Press 0 or Exist Interactor button to confirm change

When the Adjust Box is unchecked, the bounding box will the the same as last time when you defined a box, or the default one if it's never defined.

Also, the width of the bounding box can be detected using QR-Code. If the object in the scene is marked by QR markers, the initial width and depth of the bounding box will be determined by
3 QR markers.

.. image:: Images/cloud_process/cloud_process_qr_code.png
   :align: center
|

Color Filter
~~~~~~~~~~~~

The Color Filter Operation can filter out or keep the color that is selected from the scene. 

The step of picking a color and define a threshold are:
1. Define if you want to keep(Include) or remove(Exclude) the points with the color you select.
2. Input the RGB value or click the Pick Color button to pick a color from the screen.
3. Set the Color Threshold. If the RGB value of a point in the scene falls inside the range of Color Spec +/- Threshold * 10. This point will be Exclude/Include in the scene.

.. image:: Images/cloud_process/cloud_process_color_pick.png
   :align: center

Merge Point Clouds 
~~~~~~~~~~~~~~~~~~

This operation takes in another point cloud as an input and merge these two point clouds. You are also able to define the pose of the second point cloud. The below image shows merging 
two point clouds with the second one being translated along z axis.

.. image:: Images/cloud_process/cloud_process_merge_point_cloud.png
   :align: center
|

Depth Inpainting & Smoothing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Apply smoothing to and inpaint the depth image of the input point cloud. This operation helps to reduce the noise in the point cloud

Depth Diff
~~~~~~~~~~

Subtract points from the input cloud using cloud b.

* Cloud b The cloud we are subtracting from the input. Result is input cloud - cloud_b.
* Distance Threshold: The allowable depth difference between corresponding points for them to be considered to have the same value. Larger values remove more points.

Apply Mask 
~~~~~~~~~~

Apply a 2d mask to the point cloud.

* Mask: Mask Image, the point cloud has to be organized and the mask image must have the same width and depth with the point cloud

Set Reference Frame 
~~~~~~~~~~~~~~~~~~~~

Define a reference coordinate using the interactor.

.. image:: Images/cloud_process/cloud_process_reference_frame.png
   :align: center
|

Procedure to Use
----------------

1. Make sure you have a Camera node or reader node which outputs pointCloud, and insert a Cloud Process Node.
      .. image:: Images/cloud_process/step_1.png

2. Link the input Point Cloud.
      .. image:: Images/cloud_process/step_2.png

3. You may optionally change the RGB Restore settings or check Advanced check box

4. Click the '+' sign to add an operation, and in the drop down menu, select where to insert the operation.
      .. image:: Images/cloud_process/step_4.png

5. Double click on the created operation, at the top you may select from a list and change the operation type.
      .. image:: Images/cloud_process/step_5.png

6. Adjust the operation settings accordingly (see above section "Operations and Parameters" )

7. Click Done and run the node.

Excercise
---------

Try to come up with the setting on **Cloud Process** node according to the requirements below. 
You can work on these exercise with the help of this article. We also have answers attached at the end of this exercise.

This is some helpful resource when you are working on the exercise:

Scenario 1
~~~~~~~~~~

There is a project which requires you to prepare and preprocess the pointCloud for further flowcharts. 
Your colleague has setup the 3D camera for experiment. 
Here's a `link to .dcf file <https://daoairoboticsinc-my.sharepoint.com/:u:/g/personal/tzhang_daoai_com/EUaL8LFp-JlJugrB-VYSCr8BODvs7cyJszjIywupMCNDDg?e=XCPFjb>`_ 
which are used as camera input.

You need to help him setup the **Cloud Process** node in main_flowchart. Please choose the all correct answers from the options:

1. suppose the input pointCloud is really big, and you want to reduce the size of the pointCloud to speed up later computations.
What operations can you use? 

   A. Downsample or Outlier Removal
   B. Dynamic Box Filter or Color Filter
   C. Crop a Region or Adjust Bounding Box
   D. All of the above

2. Suppose you are asked to cut out a region of interest in the pointCloud. Which operation is the most easiest to acchieve this?

   A. Crop a Region
   B. Adjust Bounding Box
   C. Dynamic Box Filter
   D. Transform Coordinates

3. Your partner has used Adjust Bounding Box operation to obtain an object model from the scene. But the model's center of axis is far away 
from the object. How can you help him to bring the center of axis onto the object?

   A. add a Set Reference Frame operation and move the axis on the object.
   B. add a Transform Coordinates Operation and link to a transformation tree which computes the inverse.
   C. Both A & B.
   D. None of the above.


|
|
|
Answers for Excercises
~~~~~~~~~~~~~~~~~~~~~~

Scenario 1
```````````````

1. **Answer: D**

**Explanation**: All of the mentioned operations can reduce the size of the pointCloud.

2. **Answer: B**

**Explanation**: Adjust Bounding Box allows you to edit a box on display window, and everything inside the box will be kept. It is the most commonly used operation for capturing an
area of interest.

3. **Answer: B**

**Explanation**: Set Reference Frame only sets an reference axis, it does not change the point cloud's coordinate. Whereas Transform Coordinates applies transformation on the pointCloud.









