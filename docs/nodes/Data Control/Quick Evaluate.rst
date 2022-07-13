Quick Evaluate
==============
The Quick Evaluate page can be accessed as another tab alongside 'Console' and 'Recipes'. It can be used to evaluate expressions referring to values in the workspace. 

 .. image:: images/quick_evaluate.png
	:scale: 45%	
	:align: center
	
Expressions can be added to the evaluation table by selecting one in the 'Available Expressions'. The expressions can be modified once inside of the evaluation table in order to add in an index or map key, such as would be required for expressions containing in [] (vector requiring integer index) or [''] (map requiring string key).

As the flowchart runs, the expressions will be continuously evaluated and refreshed to reflect their changing values.  

Usage Example
=============

View the detail pose of a found object in the Reconstruct node.

The flowchart has a Camera node to input image and a Mod Finder node to find tee.
 
 .. image:: images/quick_1.png
	:scale: 50%	
	:align: center

Pass the result to Reconstruct node to get 3D poses.

 .. image:: images/quick_2.png
	:scale: 50%	
	:align: center

Click the "Quick Evaluate" to open the section and click the triangle on the left of the reconstruct.

 .. image:: images/quick_3.png
	:scale: 50%	
	:align: center

Expand the "objectPositions", then select the "occurrence[]". The expression represents the object position of the selected object.

 .. image:: images/quick_4.png
	:scale: 50%	
	:align: center

Click the Pose under the "Evaluated Value". There is no pose in the "Evaluated Result" because the index of occurrence is empty. The software does not know which pose to return.

 .. image:: images/quick_5.png
	:scale: 50%	
	:align: center

If the target object is the tee on the top left, its index is 0. Enter 0 in the bracket of the occurrence under the "Expression" section.

 .. image:: images/quick_6.png
	:scale: 50%	
	:align: center

Click on the "Re-Evaluate" to run the modified expression. "View More" to see the result.

 .. image:: images/quick_7.png
	:scale: 50%	
	:align: center

The pose is shown in the "Evaluated Result" window.

 .. image:: images/quick_8.png
	:scale: 50%	
	:align: center