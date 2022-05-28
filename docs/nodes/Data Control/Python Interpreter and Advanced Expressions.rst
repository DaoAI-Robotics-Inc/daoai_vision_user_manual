Python Interpreter and Advanced Expressions
===========================================
A python interpreter is used in the evaluation of Advanced Expressions. An Advanced Expression is a way a you can define an input by writing short snippets of simple code which can reference other pieces of information in the system, such as the fields stored in a Constant Node or the number of models found in the Mod Finder V2 Node. An example of an advanced expression is shown below:

.. image:: images/simple_advanced_expression.png
	:scale: 80%	

In this expression, if the value stored in the integer field of the Constant Node in the flowchart main_flowchart is greater or equal to 5, the advanced expression evaluates to True, otherwise it evaluates to False. 

Here is another example of an advanced expression which returns different Point Clouds based on if a 3D Model Finder Node performed a successful detection:

.. image:: images/object_advanced_expression.png
	:scale: 80%	

Advanced expressions are evaluated using a Python Interpreter, so all logic used must follow Python syntax (':' after 'if' statements, proper tabbing, etc), however advanced expressions must also contain a 'RETURN' keyword to signify what the output of the expression should be. 

Other keywords specific to DaoAI Advanced Expressions are INT((...)), DOUBLE(...), BOOL((...)), STRING((...)), and OBJECT((...)) which are used to evaluate expressions referring to data in other nodes of the system. 

Usage Example
--------------

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
