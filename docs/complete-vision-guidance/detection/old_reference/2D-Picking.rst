2D Detection
==========

It is mainly designed for detecting the precise location of object to be picked. It uses image RGB to detect object location.

``Mod Finder`` Node takes ``Image`` Node result as input and you are able to define the object model. 
Defining a good model is essential for Detection, a good model can help the system to identify the objects in many different situation. But note that, machine is still machine, some object might be different from front and back, system only able to identify the model which you defined. As example, template is a sample project which is looking for the T-tubes. The T-tubes are identical front and back. Hence, the system is able to detect both sides. 
Mod Finder Node is detecting object from image RGB and depth. When adding Mod Finder Node, system will ask which source to use.
2D is taking image RGB as input, and 3D is depth image. In this case, system takes RGB image as input, so that choose 2D. Console with print the message with how many objects found, also displaying the object in the image. 

.. image:: Images/2d_detect.png
    :align: center
    
|

Image link is the input user-defined for Mod Finder Node. Checking the ``Use labelled mask sequence`` enables the node to use designated mask for the models; commonly taking Deep Learning ouput(DL Segment Node). Total occurence option can be detect all the objects in the image or only one object in the image at a time: if you want to pick all occurence of objects with single image captured, this option should set to ``All``; on the other hand, picking one object at a time should set to ``One`` (default).
Double click on the model name brings up the Model Param Configuration dialog. There are more parameter settings for the model in this dialog. Mod Finder Node uses the model details to detect the objects in the image. 
``Draw Mask`` is able to set a excluding area for the model, the mask area would be ignored when it comes to detect the object. 
``Erase Mask`` can erase the drawn area. Reference point is generated at the middle of the object by default. Reference point would be used by Reconstruct Node, generating Z coordinate from this point. 
``Define Red Point`` allows you to define a new reference point on the object. It is useful when the object is skewed or heavy on one side: robot might be failed to grab or the object will fall when using this reference point. 
``Acceptance`` is the acceptance level for the system: if the acceptance level is too high, system might not be able to detect all the objects since system sees the objects in the image is not 100% identical to the model. On the other hand, low acceptance level might lead to finding too many objects, system might detect all the similar points, pixels in the image as the object. You should adjust the acceptance level to detect all the occurrence AND as high as possible. 

In 2D Picking, we can use ``Calibration 2D`` Node to generate the reference point for objects. Choosing ``Project`` mode, taking ``Image`` and ``Mod Finder`` results as inputs, referring with Calibration Node. 

.. image:: Images/2d_cali_p.png
    :align: center
    
|

As shown above, the green circles would be the gripping points for robot.
