Picking Multiple Objects
==============

In the following image example, there are many different kinds of object; if requirement asks to pick different specific type of object at each different iteration, you are able to alter the system to archive this.

.. image:: Images/teabag.png
    :align: center
    
|

Recipe & Payload
------------

In the bottom console window, there is a tab ``Recipes`` . In this tab, we can ``Add Recipe`` and matches the number of different objects we want. For example, if we have 14 different objects to choose, then we need 14 recipes to switch between these objects.

.. image:: Images/console.png
    :align: center
    
|

``Payload_2`` is the variable to control which object to pick. In Picking flowchart, ``Load Recipe`` Node would take the robot payload_2 as input, determine which recipe to load.

.. image:: Images/payload_2.png
    :align: center
    
|

Adding ``Payload_2`` as the input for ``Load Recipe`` , opens up the link dialog from ``Selected Index`` , choose the corresponding link for ``Load Recipe`` Node.

.. image:: Images/link_payload.png
    :align: center
    
|

Note: When running the Teach_Pose flowcharts, you needs to teach all the different recipes: for example, if we have 14 different recipes, we need to teach all the recipes ``Gripper`` to produce all the different poses for different objects.

.. image:: Images/load_teach.png
    :align: center
    
|

Even though different recipes are for different objects, but basically all the them running with common procedures. Only some of the nodes would process different values, these nodes are added to the recipe.

.. image:: Images/add_recipe.png
    :align: center
    
|

And only these nodes, switching recipes would switch their inputs or configuration. These nodes have a small ``R`` logo on it like the image shown below.

.. image:: Images/recipe_node.png
    :align: center
    
|

