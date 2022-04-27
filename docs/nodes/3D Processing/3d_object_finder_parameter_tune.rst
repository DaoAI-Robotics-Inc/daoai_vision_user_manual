Parameter Tunning Guide
---------------------------

This guide will walk through some rules of thumb when it comes to adjusting parameters to get better detection.

Not detection all objects
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Increase the search detail. This will increase the number of computed scene features
* Decrease acceptance threshold. This lowers the acceptance threshold of the score filter, keeping poses with lower scores

.. image:: Images/3d_obj_finder/search_detail_low.png
   :width: 100%

.. image:: Images/3d_obj_finder/search_detail_high.png
   :width: 100%

.. image:: Images/3d_obj_finder/acceptance_low.png
   :width: 100%

.. image:: Images/3d_obj_finder/acceptance_high.png
   :width: 100%

False positive
~~~~~~~~~~~~~~~~~~~~~~~~~~

* Reduce downsample strength. This makes the downsample voxel size smaller, preserving more detail in the scene. Reducing downsample strength can also improve poses that are badly oriented.

.. image:: Images/3d_obj_finder/downsample_low.png
   :width: 100%

downsample strength low

.. image:: Images/3d_obj_finder/downsample_medium.png
   :width: 100%

downsample strength medium

Model parameters
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Adjust model feature detail. Increasing model feature detail will increase the amount of model features calculated, making it more likely to accurately find the object in the scene
* Adjust model downsample strength. Reducing downsample strength can remove false positives


.. image:: Images/3d_obj_finder/feature_detail_low.png
   :width: 100%

feature detail low

.. image:: Images/3d_obj_finder/feature_detail_high.png
   :width: 100%

feature detail high

.. image:: Images/3d_obj_finder/model_downsample_low.png
   :width: 100%

downsample strength low

.. image:: Images/3d_obj_finder/model_downsample_medium.png
   :width: 100%

downsample strength medium