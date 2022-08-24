Shape Finder Node 
=========

Overview 
--------------------
Shape finder node is used to find shapes on gray scale images using edge based searching. 

.. image:: images/shape_finder_overview.jpg
   :scale: 90%

Input and Output 
-----------------

+----------------------------------------+-------------------------------+-------------------------------------------------------------------------------+
| Input                                  | Type                          | Description                                                                   |
+========================================+===============================+===============================================================================+
| Image                                  | Image                         | The source that is used to search for shape.                                  |
+----------------------------------------+-------------------------------+-------------------------------------------------------------------------------+
| Time out                               | Int                           | Time in miliseconds that the shape finder will search before terminatation    |
+----------------------------------------+-------------------------------+-------------------------------------------------------------------------------+

+-------------------------+-------------------+------------------------------------------------------------------------+
| Output                  | Type              | Description                                                            |
+=========================+===================+========================================================================+
| labelledPose2dSequence  | Vec<Pose2D>       | Vector of pose 2d preserving order from labelled mask sequence.        |
+-------------------------+-------------------+------------------------------------------------------------------------+
| shapeMasks              | Map<Image>        | A map of model masks. (Mask is created using the shapes edges)         |
+-------------------------+-------------------+------------------------------------------------------------------------+
| shapeLocation           | Map<Vec<Pose2D>>  | A map of vector of 2d shape locations (Pose2D of shape center).        |
+-------------------------+-------------------+------------------------------------------------------------------------+
| numFound                | Int               | The total number of Shapes found.                                      |
+-------------------------+-------------------+------------------------------------------------------------------------+
| success                 | Bool              | Boolean value indicating the search is successful.                     |
+-------------------------+-------------------+------------------------------------------------------------------------+


Node Settings
---------------

The following image demonstrates the shape finder node settings

.. image:: images/shape_finder_settings.png
   :scale: 100%

Source Parameters
~~~~~~~~~~~~~~~~~

- **Image**:

   The source that is used to search for shape. Using link expression to link the image.

- **Time Out** (Default value: 2000 ms):

   The time limit for the node to run. When the running time of the node reaches the time limit. The node will terminate and return the current output.


Shape finder settings
~~~~~~~~~~~~~~~~~~~~

- **Create Solid Mask**:

   By defualt the output mask only includes the detected shape edges. When checked, the output mas will be filled to create a solid mask.

- **Use Reference Fixture**:

   This node can be used for generating fixture.
   Please refer to `Reference Fixture System <https://daoai-robotics-inc-daoai-vision-user-manual.readthedocs-hosted.com/en/latest/nodes/DA%20Modules/Reference%20Fixture%20System.html>`_.

Algorithm Parameters
^^^^^^^^^^^^^^^^^^^^

- **Speed** (Default value: MEDIUM):

   The speed of searching. Larger value means faster speed but less accuracy.

- **Accuracy** (Default value: MEDIUM):

   The accuracy of searching. Larger value means heigher accuracy but slower speed.

Shapes
~~~~~~

General Settings
^^^^^^^^^^^^^^^^

	.. image:: images/shape_finder_shapes_general.png
		:scale: 90%

- **Name**:

   Name for the shape created, you can give whatever name you like.

- **Dedicated Mode** (Default value: No):

   Use a dedicated algorithm and the search_region, scale, and speed settings will be ignored if choosing yes.

- **Shape** (Default value: Circle):

   List of shapes available for shape finder.

- **Foreground Color**:

   The color of area within the shape to be accepted as a occurrence. 

- **Param[2-5]**:

   Parameters on shape dimensions, the unit used here is in **pixels**
   | number of parameter needed varies on different shapes.

- **Min Acceptance** (Default value: 60): 

   The minimum matching score where an occurrence is accpeted. 
   An occurrence will be returned only if the match score between the target and the model is greater than or equal to this level.

- **Total Occurrences** (Default value: One): 

   Maximum number of Shapes to search before terminatation.
   When the number of found matching shapes is equal to the set Total Occurrences value, the node will terminate and return the current result.

- **Whole Image** (Default: Checked):

   When checked, the node finder will search on the whole image.
   When unchecked,  the node finder will search on the restricted area of the image that you need to define.

- **Enable Search Scale** (step: 0.1): 

   When checked, the node finder will also search on scaled image of the input image from scale Min to Max with a step of 0.1.
   When unchecked, the node finder will only search on the input (non-scaled) image.

Advanced Settings
^^^^^^^^^^^^^^^^^

	.. image:: images/shape_finder_shapes_advanced.png
		:scale: 90%

- **Smoothness** (Range[0-100], default: 50):

   Sets the degree of smoothness (noise reduction) applied to the model images and target images during the edge extraction.
   | A setting of 0 indicates almost no noise reduction effect, while a setting of 100 indicates a very strong noise reduction effect.

- **Detail Level** (Default value: Medium):

   Sets the level of details to extract from model images and target images during edge extraction.
   | The detail level determines what is considered an edge/background.
   | A heigher detail level will include more edges than a lower detail level.

- **Certainty** (Range[0-100], default: 90):

   Sets the certainty level for the score, as a percentage.
   | If both the score and target scores are greater than or equal to their respective certainty levels, the occurrence is
   considered a match, without searching the rest of the target for better matches.
   | Higher certainty results in better accuracy but lower running speed. A good certainty level should be slightly lower than the
   expected score, so that the search terminates as soon as a match is found.

- **Polarity** (Default value: Same Or Reverse):

   Sets the expected polarity of occurrences, compared to that of the model.
   | "Same" means the foreground should be same as you specified.
   | "Reverse" means the foreground color is reversed.
   | "Same Or Reverse" means all that is "Same" or "Reverse".
   | "Any" means you do not care about the foreground color.

- **Fit Score Min** (Range[0-100], default: 0):

   Only supported in dedicated mode.
   | Sets the minimum expected occurrence fit score.

- **Sagitta Tolerance** (Range[0-100], default: 25):

   Only supported in dedicated mode for Circle or Ellipse.
   | Sets the tolerance for finder deformed circles (allowable radii variation) for a model.
   | A value of 0 means that the circular shape being sought needs to be as close as possible to a perfect circle.
   | A value of 100 means that the algorithm as the maximum tolerance for finding deformed circles.

- **Coverage Max** (Range[0-100], default: 100):

   Only supported in dedicated mode for Circle or Ellipse.
   | Specifies the maximum expected model coverage.


Procedure to use
-----------------

1. Open a workspace in DaoAI Vision Studio.
	
   .. image:: images/mod_finder_procedure_1.png
      :scale: 30%

2. Insert a Camera node to get the source image.
	
   .. image:: images/mod_finder_procedure_2.png
      :scale: 60%

3. A virtual image is used to demonstrate. Refer to System Overview, Tutorials on how to connect to camera.
	
   .. image:: images/shape_finder_step_3.png
      :scale: 50%

4. Add a Shape Finder node after the camera node
	
   .. image:: images/shape_finder_step_4.png
      :scale: 50%

5. Link the input Image to Camera node output
	
   .. image:: images/shape_finder_step_5.png
      :scale: 50%

6. Click the '+' sign to add a shape, give it a name you prefer and click confirm
	
   .. image:: images/shape_finder_step_6.png
      :scale: 70%

7. Double click the shape you just created, select a shape, and fill in the params, you can also adjust other settings, close the window when you are done.
	
   .. image:: images/shape_finder_step_7.png
      :scale: 50%

8.  Select the Shape Finder node if its not selected already, and click run select step, then you should see the result on the left view port.
	
   .. image:: images/shape_finder_step_8.png
      :scale: 50%


General process of Using Mod Finder Node
----------------------------------------

1. Link input image. 

2. Run node once so the input image shows on the display.

3. Define shape, click on “+” button to add a shape, and select a shape to be searched in the image and input its parameters.

4. (Optional) adjust other shape settings or Advanced settings in the shape config page.

5. Run the node with other images. The found occurrences of the shape will be displayed in the target image.

6. Use the position vector for further processing to get the picking pose of the objects in the scene.

Excercise
---------

Here is a `link to a .dcf file <https://daoairoboticsinc-my.sharepoint.com/:u:/g/personal/tzhang_daoai_com/EagIObWqB4tCtzCcq5dDaWIBcV0UEiF18-smQlPup_1UjQ?e=OYTXZx>`_.

Try to create your own workspace and find all the objects in the .dcf with a shape finder node.



