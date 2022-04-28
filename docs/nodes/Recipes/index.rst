Recipe nodes
========================

This section contains basic introduction about the concept of the recipe and how to use the 
recipe nodes.

Processing Nodes Vs Definition Nodes
--------------------------------------

Processing nodes are nodes that doesn't require re-configuration in field. For example, camera nodes. Due to such reason these nodes are not able to store configuration in recipe
Definition Nodes, on the other hand, are nodes that may have changing configuration in field application, or their configuration requires user interaction (such as adjust 
bounding box filtering in cloud process node). These nodes are able to store information in the recipe.

Complete List of Definition Nodes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Mesh Process
* Calibration
* Mod Finder 
* Sphere Calibration
* Reader
* Hand Eye Calibration 2d
* Hand Eye Calibration 2d V2
* Calibration 2d
* DA Calibration
* Gripper
* Assemble possible
* DL segmentation
* DL classification
* Object Finder 3d

An Exmaple on How to Use the Recipe Feature
--------------------------------------------

We use this simple workspace to illustrate how we can use recipe. In this workspace, camera node captures a point cloud, then the point cloud is converted 
to a depth image, based on this depth image mod finder finds the 3d locations of defined objects in the camera scene. By default, we have only 1 recipe, and no
nodes store info in recipe now.

.. image:: Images/Workspace.png
   :align: center

Add/Remove Recipe, Add Node to Recipe
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

From the recipe panel on the bottom of the mainwindow you can add and remove recipe. To tell a node to store its information in recipes, right click on the node
and select "Add Node To Recipe". Once that's successful, you will see a small R icon on the top left of the node.

.. image:: Images/add_node_to_recipe.png
   :width: 40%

Switch Recipes
~~~~~~~~~~~~~~~~~~~~~~~~

Now we have two recipes are we want to define a model for mod finder node for each recipe. In recipe 1,
We run the flow chart from the start to mod finder node, and define a model 

.. image:: Images/model_and_scene_1.png
   :align: center

Double click recipe_2 in the recipe panel to switch to recipe_2, re-run the process to define another model

.. image:: Images/model_and_scene_2.png
   :align: center

Now switch back to recipe_1, you should see the first model in the mod finder node. Now we have two recipes to search for different models.

Load Recipe Node
~~~~~~~~~~~~~~~~~~~~~~

All the creation and definition work of the recipes must be done before the project deployed to the field. However, users are able to swith recipe automatically using the 
load recipe node.

.. image:: Images/recipe_node.png
   :width: 58%

When the load recipe node is run, it loads the recipe in its recipe table specified by the input index. You can add or remove recipe entry in the table by clicking add or remove button.
The index of the entry is unique and fixed once it is added. The recipe name of each entry and the index name to load can be manually changed or linked, giving user the flexibility
to automatically load specific recipes.