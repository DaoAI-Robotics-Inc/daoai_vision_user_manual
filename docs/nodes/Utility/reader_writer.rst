Reader Node and Writer Node
==============================

Reader Node
-------------------

.. image:: Images/util/assemble_bag.png
   :align: center

The Reader Node allows for reading common file types for use in the flowchart.

Currently, four types of files are available:
* RGB images (in .png format by default)
* Depth images (in .tif format by default)
* PCL Point Cloud (in .pcd format)
* Polygon Mesh (in .ply, .stl, .obj format)
* Bag files (.bag format)

The reader node is capable of reading from a file or folder. This node also saves the cache of files it reads so that it can load it in next time and not have to read it from an external location next time.

Three source types are available:

* Read from file: Reads from a single file
* Read from folder: Reads from files inside a folder
* Read from numbered: Reads from files with the same naming scheme ending in a number

If you chose a file with a non-supported extension, the program will give an error message. Also, if reading from a folder or in numbered orders, the program will give an error message if the folder is empty or, it does not include any of the valid extensions, or in case the more than one valid extension type exists in the folder.  

Read From a single file
~~~~~~~~~~~~~~~~~~~~~~~~~~

In this mode the node will read the same file whenever it runs, unless the specified path is changed

Read From Folder
~~~~~~~~~~~~~~~~~~~~~~~~~~

In this mode the node will iterate through all the files in the given folder and read one file in each run, this mode 
supports forward traversal (lexicographical) and backward traversal. Please note that only one type of file can be in the given folder
otherwise the reader node will not know which type of data to read. You can also reset iterator with the "reset values" button.

Read From Numbered Files 
~~~~~~~~~~~~~~~~~~~~~~~~~~

This is the more advanced version of reading from folder mode. Here you can specify the file prefix and index. For example, if the prefix is `daoai_` and index range is between
0 and 12, the node will read from daoai_0 to daoai_12, and start from 0 again. You can also reset iterator with the "reset values" button.

Output
~~~~~~~~~~~~~~~~~~~~

The output of this node will have one of these fields valid: outputBag, outputCloud, outputImage (depth or rgb), outputMesh, depending on the file being read.
It also has numOfFiles output, which indicates number of files read so far (in read from folder mode), and index, which shows the current index (in read from numbered mode).

Writer Node
-------------------

Writer nodes write certain types of data to files in disk

.. image:: Images/util/assemble_bag.png
   :align: center

Different from the reader node you have to choose which type of data you want to store. Like reader nodes, writer nodes also have single file mode and numbered file mode.

Input
~~~~~~~~~~~~~~~~~~~~~

One of RGB image, depth image, point cloud, mesh, bag.



