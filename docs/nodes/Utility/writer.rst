Writer Node
===============

Overview
-----------

**Writer node** writes various types of data to files in disk.
There are two modes available for writing data: From File, and From Numbered.
If there are files with the same name when writing new files, the old files will be overwritten.

.. image:: Images/util/writer_overview_1.png
   :align: center

.. image:: Images/util/writer_overview_2.png
   :align: center

|

Input
------------------

+----------------------------------------+-------------------------------+---------------------------------------------------------------------------------+
| Input                                  | Type                          | Description                                                                     |
+========================================+===============================+=================================================================================+
| Source Type                            | Point Cloud                   | The Point Cloud from scene (Camera, Reader etc.).                               |
+----------------------------------------+-------------------------------+---------------------------------------------------------------------------------+
| Data Type                              | Vector<Poses>                 | The results of poses. Usually from Mod Finder, Reconstruct etc.                 |
+----------------------------------------+-------------------------------+---------------------------------------------------------------------------------+

|

Node Settings
--------------

.. image:: Images/util/writer_node_settings.png
   :align: center

**Data Source**

- Source Type (Default: From File):
    From File: write data to one single file.
    From Numbered: write data to multiple files. 

- Data Type (Default: RGB_IMAGE (.png)):
    Select from one of the four output file types:
        - RGB_IMAGE (.png)
        - DEPTH_IMAGE (.tif)
        - POINT_CLOUD (.pcd)
        - POLYGON_MESH (.ply)
        - BAG (.bag)

- Write Data:
    The data to write to files.

**Save to**

- File Path: Available in From File mode.

- File Prefix (Default: "daoai_"):

- Start Index (Default: 0):
    The starting index of the file to be saved.

- End Index (Default: 10000):
    The ending index of the file to be saved.

|

Procedure to Use
-----------------

1. Insert a Camera node, and a Writer node.