Box Volume Estimation Node
=============================

The purpose of the box volume estimation node is to analyze a vector of point clouds and generate an estimated length, width, and height of each box, as well as an appropriate picking location. It works by generating a bounding box around the segment such that it is aligned with the specified reference frame, and extending it downwards until it reaches the origin of the reference frame. The node obtains its best results when the segments are rectangular in shape, and are closely aligned to the reference frame. The node does not have any functionality for determining if a segment is “rectangular”, nor does it discriminate from non-rectangular segments (although the results will likely be poor quality). 

The poses for each box are normally generated at the center of the top face of each box. However, there are many options for customizing how these poses are generated.

.. toctree::
   :maxdepth: 1

   box_vol_est_overview
   box_vol_est_procedure
   