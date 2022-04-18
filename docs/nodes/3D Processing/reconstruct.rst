Reconstruct Node
===========================

The Reconstruction Node uses the hypothesis position of a detected object and its centroids to generate a 3D pose. 
The hypothesis position and centroid information usually comes from the Mode Finder Node. 
The 3D pose uses the model defined in Mod Finder Node as a reference to compute its translation and rotation(in camera coordinates). 
In order the visualize the pose, it will be displayed in the scene using a small XYZ axis.

.. image:: ../../_static/images/3d_process/reconstruct/reconstruct.png
   :width: 100%

.. toctree::
   :maxdepth: 1

   reconstruct_overview
   reconstruct_procedure

   