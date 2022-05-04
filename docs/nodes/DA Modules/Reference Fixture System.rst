Reference Fixture System 
=========

Synopsis 
---------
	Fixture system allows you to define a reference frame and make all other things relative to the fxiture frame.


Define Fixture 
---------
	The fixture is defined in a 2d mod finder or 3d mod finder node. 
	It is recommend to have only one model in this node. If more than 1 model defined, it will pick the one with highest score.

	For example, we define model as following. The model will generate a reference frame, and the reference frame changes along with detected obect. 
 .. image:: images/fixture_define1.jpg
	:scale: 60%
 .. image:: images/fixture_define2.jpg
	:scale: 60%
|

Use Fixture 
---------
	After you clicked the checkbox of use_fixture in a node, you can select a mod_finder node as reference.
	
	For shape_finder node and mod_finder node, you need to redefine search region for each model. The region redefine should be done on the same image of reference mod_finder node.
	
	For measurement node and metrology node, you need to relocate or redefine the search region, as their position will change with the fixture.
	
	Following images are metrology node without fixture. The blue region is the search region for searching circle.
 .. image:: images/fixture_metrology_unfix1.jpg
	:scale: 60%
 .. image:: images/fixture_metrology_unfix2.jpg
	:scale: 60%
|

	Following images are metrology node with fixture. The search region changes with the fixture.
 .. image:: images/fixture_metrology_fix1.jpg
	:scale: 60%
 .. image:: images/fixture_metrology_fix2.jpg
	:scale: 60%
|

	Following images are mod_finder node with fixture. The yellow box is the fixture object, and the blue box is the search region that changes with the fixture. 
 .. image:: images/fixture_mod_finder1.jpg
	:scale: 60%
 .. image:: images/fixture_mod_finder2.jpg
	:scale: 60%