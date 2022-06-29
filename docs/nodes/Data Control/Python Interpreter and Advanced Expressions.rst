Python Interpreter and Advanced Expressions
===========================================
A python interpreter is used in the evaluation of Advanced Expressions. An Advanced Expression is a way a you can define an input by writing short snippets of simple code which can reference other pieces of information in the system, such as the fields stored in a Constant Node or the number of models found in the Mod Finder V2 Node. An example of an advanced expression is shown below:

.. image:: images/simple_advanced_expression.png
	:scale: 80%	

In this expression, if the value stored in the integer field of the Constant Node in the flowchart main_flowchart is greater or equal to 5, the advanced expression evaluates to True, otherwise it evaluates to False. 

Here is another example of an advanced expression which returns different Point Clouds based on if a 3D Model Finder Node performed a successful detection:

.. image:: images/object_advanced_expression.png
	:scale: 80%	

Advanced expressions are evaluated using a Python Interpreter, so all logic used must follow Python syntax (':' after 'if' statements, proper tabbing, etc), however advanced expressions must also contain a 'RETURN' keyword to signify what the output of the expression should be. Other keywords specific to DaoAI Advanced Expressions are INT((...)), DOUBLE(...), BOOL((...)), STRING((...)), and OBJECT((...)) which are used to evaluate expressions referring to data in other nodes of the system. 

Other keywords specific to DaoAI Advanced Expressions are INT((...)), DOUBLE(...), BOOL((...)), STRING((...)), and OBJECT((...)) which are used to evaluate expressions referring to data in other nodes of the system. 

Templates
---------
There are several types of frequently used advanced expressions, copy them and make changes according to your workspace.

Condition Check
~~~~~~~~~~~~~~~
This is a typical condition check exist in many of the robot command checking switch nodes. 
Changes: 
1. The INT((../command)) should be the value you want to check.
2. The "21" should be the value that you want to compare to your first line.
3. You can also change the "==" to ">, <, <= , >=, !=" for diffenent situation.


.. code-block:: python
   	:linenos:

   	condition_name = INT((Out/main_flowchart.robot_read_node/command))
	return_value = False
	if condition_name == 21:
		return_value = True
	RETURN return_value


Return idnetifier based on conditions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Sometimes when the input link to an identifier like (Pose, point cloud, etc.), you might find there should be different inputs based on some kinds of conditions. In this case, you can use the below template.
Changes:
1. Change the condition_name to whatever your condition is.
2. The second line is the default value, which means if condition_name is something other than 1 or 2, the second line will be the return value.
3. Change the statements after "if" to fit your condition check. If you have less or more values to check, just add/remove two lines (if ... : return_value = ...)
4. change the return_value according to what you want to put into the link.

.. code-block:: python
   	:linenos:

	condition_name = INT((Variables/teach_pose.calibration_type))
	return_value = OBJECT((Out/teach_pose.switch3.fcase_default.switch.fcase_default.da_calibration_node/camInBase))
	if condition_name == 1:
		return_value = OBJECT((Out/teach_pose.switch3.fcase_default.switch.fcase_2.calibration_node/camInBase))	
	if condition_name == 2:
		return_value = OBJECT((Out/teach_pose.switch3.fcase_default.switch.fcase_1.sphere_calibration_node/camInBase))	
	RETURN return_value

Return string for printing or path
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Although it's not frequently used, but path operations are also supported. Basically you can make combinations of strings to form a path in the advanced expression.
Changes:
1. If you want to have a path, you will need to copy and paste the system path in your file exporer and change every "\" to "\\".
2. If you want to change other types like INT or DOUBLE to a string, use "variable_name = str(your_int_name)" just like shown below.
3. you can use a `+` sign to append the strings.

.. code-block:: python
   	:linenos:

	condition_name = INT((Out/teach_pose.constant_node/Int))
	path_front = "D:\\Utils\\Calibrations\\Eye To Hand\\1207_Sphere_0.37\\bag\\daoai_"
	index = str(condition_name)
	path_end = ".bag"
	return_path = path_front + index + path_end
	RETURN return_path


Use count to select vector index
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Sometimes you might need to select certain object inside a vector with different index. Therefore you should not use a fixed index like frequently used `occurrence[0]`.
Changes:
1. replace the first line my_count = xxx to your desired index.
2. change the return_object to what you want to return in this expression. but with the dynamic occurrence[].
3. Optional: Sometimes you might want to make changes to my_count variable like + 1. Then you should make the change between first and second line. For example, my_count = my_count + 3. Be sure that number will be a valid index (non-negative).

.. code-block:: python
   	:linenos:
	my_count = INT((Out/main_flowchart.count/Count))
	return_object = OBJECT((Out/main_flowchart.mod_finder_node/labelledPose3dSequence/occurrence[my_count]))
	RETURN return_object

Break loop
~~~~~~~~~~~

Looping 50 times.

.. image:: images/advanced_expression_1.png
	:scale: 70%
	:align: center

.. image:: images/advanced_expression_2.png
	:scale: 70%
	:align: center


Check Variable value
~~~~~~~~~~~~~~~~~~~~

Using variable value as switch case conditions.

Setting up the variable.

.. image:: images/advanced_expression_3.png
	:scale: 70%
	:align: center

.. image:: images/advanced_expression_6.png
	:scale: 70%
	:align: center

Case 1

.. image:: images/advanced_expression_4.png
	:scale: 70%

Case 2

.. image:: images/advanced_expression_5.png
	:scale: 70%
	:align: center

Robot Command Input
~~~~~~~~~~~~~~~~~~~

Reading the status of a robot, and react on different status.

Using a Robot Read node to read the command from robot.

.. image:: images/advanced_expression_7.png
	:scale: 70%
	:align: center

Robot Command: 20 (RC_DAOAI_CAPTURE_AND_PROCESS ). The flowchart moves to the next stage.

.. image:: images/advanced_expression_8.png
	:scale: 70%
	:align: center

|

Limitations
-----------
Due to technical problems, there are things that our system do not support yet. Try to work around them.

If inside if
~~~~~~~~~~~~
We do not support this format yet, but you can always use combinations of condition to achieve what you want.

.. code-block:: python
   	:linenos:
	#Wrong
	if a == b:
		if a == c:
			ret = something

	#Workaround
	if a == b and a == c:
		ret = something
