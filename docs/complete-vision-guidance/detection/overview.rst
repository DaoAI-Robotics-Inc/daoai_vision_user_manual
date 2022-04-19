Detection
==============

General engines
~~~~~~~~
DaoAI has two general detection engines, each optimized for a different type of shapes.

* **Mod Finder** engine is fast and robust, it is recommended detection for most applications where the object is usally one side showing to the camera. Checkout these articles for `Gray Mod Finder <https://daoai-robotics-inc-daoai-vision-user-manual.readthedocs-hosted.com/en/latest/complete-vision-guidance/detection/mod-finder/gray-mod-finder.html>`_ and `Depth Mod Finder <https://daoai-robotics-inc-daoai-vision-user-manual.readthedocs-hosted.com/en/latest/complete-vision-guidance/detection/mod-finder/depth-mod-finder.html>`_
* **3D Object Finder** engine is slightly slower, and it is recommended detection for random bin picking situations, where the object's showing face is different.
* **Mono 3D** engine is using a single 2D camera for high accuracy 3D object locating. It is suitable for eye-in-hand situation, and able to achieve better than 3D camera accuracy for single object.
* **Shape Finder** engine is suitable to find specific shapes on the images, and use it for robot guidance. It can detect shapes like circle, rectangle, ellipse etc.. 

.. tip:: You can learn about the main ideas behind the Teach engine by watching this video tutorial. (TODO)

.. toctree:: 
    :hidden:

    mod-finder/mod-finder-overview
    mono-3d
    mod-finder/good_model

Deep learning engines
~~~~~~~~~
DaoAI also offers detection engines optimized with deep learning techniques for specific part shapes and arrangements:

* **Boxes**, which is specially designed for detecting box on a pallet.
* **AnyPick**, which is specially designed for picking any type of object outside from the bin, it doesn't pick the same location everytime for any part, but it tries to pick from any pickable region.
* **KeyPoint**, which is designed for detecting object that hard to use general engines and reduce the time you configure the detection parameters. The overall logic allows user to annotate the point on the object, then it can predict the object position out from the points on the image.  

.. toctree:: 
    :hidden:

    boxes/overview
    shape-finder/overview

Other engines
~~~~~~~~~~~~~
DaoAI offers other engines which allow users to configure for specifc project:

* **Measurement & Metrology**, it allows the users to measure the object size, shape etc. 
* **Code Reading**, it allows users to detect the code from the image. 
* **2D Finder**, it allows users to achieve 2D part locating  

