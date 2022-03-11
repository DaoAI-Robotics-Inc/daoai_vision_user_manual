Detection
==============

General engines
~~~~~~~~
DaoAI has two general detection engines, each optimized for a different type of shapes.

* **Mod Finder** engine is fast and robust, it is recommended detection for most applications where the object is usally one side showing to the camera. 
* **3D Object Finder** engine is slightly slower, and it is recommended detection for random bin picking situations, where the object's showing face is different.

.. tip:: You can learn about the main ideas behind the Teach engine by watching this video tutorial. (TODO)

Deep learning engines
~~~~~~~~~
DaoAI also offers detection engines optimized with deep learning techniques for specific part shapes and arrangements:

* **Boxes**, which is specially designed for detecting box on a pallet.
* **AnyPick**, which is specially designed for picking any type of object outside from the bin, it doesn't pick the same location everytime for any part, but it tries to pick from any pickable region.
* **KeyPoint**, which is designed for detecting object that hard to use general engines and reduce the time user configure the detection parameters. The overall logic allows user to annotate the point on the object, then it can predict the object position out from the points on the image.  

