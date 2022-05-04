Procedure of Using Mod Finder Node
========================================

1. Link input model image. For 3d mod finder node, the input must be the output of DA CloudNDepthConv Node.
2. Run node once so the input image shows on the display.
3. Define model, click on "+" button to add a model, and draw a bounding box in the input image to define the model.
4. (Optional) adjust model in the model config page.
5. Run the node with other images. The found occurrences of the model will be displayed in the target image.
6. Use the position vector  for further processing to get the picking pose of the objects in the scene.

Model Configuration
-------------------------

You can adjust the detail of the model in the model config page. Double click or select model and click edit button to open model config page.

 .. image:: images/mod_finder_config.png
	:scale: 60%

The red lines are the extracted edges of the model, which will be used for searching. You can mask out or unmask area that you are not interested in by clicking "Draw Mask" or "Erase Mask" button.
This will enter interactor mode where you can edit mask. You can also change "Edit Pixel Map Size" to change the brush size when drawing and erasing mask.

You can also define reference point in the model image by clicking "Define Ref Point" of the model. This will enter interactor mode where you need to select a point as a reference point.
Normally the reference point is the center of all the edge pixels. It is recommended to use the default reference point.

Additionally, you can define the search region in the target image by clicking "Define Search Region" and draw a rectangle ROI on target image.

Search Model In Labelled Mask Sequence 
--------------------------------------

This is a special use case of mod finder where the input is the result of segmentation (a vector of image, each contains an object) instead of a single image.

1. Use DL segmentation node to obtain segments and their labels.
2. In mod finder node, define models. Assign correct labels to the models.
3. Check "Use Labelled Mask Sequence", and link the labelled mask sequence to mask sequence output of of the DL segmentation node.
4. Run the node. For each mask image in the sequence the node will search for the model based on the model of the mask image (label of the segment).
5. The result pose (sorted in labelledPose2dSequence or labelledPose3dSequence) will have the same order of the segments vector of the DL segmentation node.