3d Object Finder Node
==========================

This node is used to find 3d locations of an object using PPF related algorithms.
At the creation of the node, users need to select which type of PPF to use (normal PPF or edge PPF mode).

Input 
-----------------------

Scene cloud: one or a vector of point clouds to find objects within.

Output
-----------------------
cloudModel: active model used for searching, represented as point cloud
edgesModel: active model used for searching, represented as edge cloud. Available only in edge mode
msehModel: active model used for searching, represented as mesh. Available only when the model is defined by mesh
resultPoses: a vector of pose represeting the result of search
success: a field indicating whether the search is successful (at least one position found)

Model Creation and Processing
------------------------------------
Users can create multiple models that can then be searched for within the scene.
Additionally, users can use the adjust pose interactor to modify the model pose or the define search region interactor to modify the search region used to search for that specific model.

Model Parameters:

* Define type : int
   * How the model will be defined, either “from mesh” or “from scene”
* Mesh path : string
   * Mesh path used when define type is “from mesh”
* Export path : string
   * Path used when exporting the model
* Feature detail : int
   * Controls the amount of model features calculated
* Downsample strength : int
   * Controls the strength of the downsample filter applied to the model
* use search region : bool
   * Controls whether to use the user-defined search region
* constrain x-axis/y-axis/z-axis rotation : bool
   * Controls whether to enable x/y/z axis rotation constraints when searching for object poses
* min angle : double
   * Minimum rotation angle about the x/y/z axis when searching for object poses
max angle : double
   * Maximum rotation angle about the x/y/z axis when searching for object poses

3D Detection 
--------------------

When the 3D Object Finder Node in run, the node will search for instances of the selected model and output the poses found.

Scene Matching Parameters:

* Search type : int
   * Type of search algorithm used, either Normal or Edge PPF
* Selected model : string
   * The name of the model that will be searched for 
* Downsample strength : int
   * Controls the strength of the downsample filter applied to the scene
* Search detail : int
   * Controls the quality of the search. Larger values mean more thorough search.
* Object separation : int
   * Controls expected distance between target objects. Larger values mean more separation expected between objects.
* Timeout : double
   * Timeout in ms
* Acceptance threshold : double
   *Controls the threshold used when filtering possible poses.

Edge Extraction
--------------------
When the search type is set to Edge, we perform edge extraction on both the model and scene 

Edge Parameters:

* Enable NaN edges : int
* Enable RGB edges : int
* Enable Occluding edges : int
* Enable Depth Edges : int
* rgb detail : int
   * The rgb edge detail level, larger values provide more edges.
* depth detail : int
   * The depth edge detail level, larger values provide more edges.
* occluding detail : int
   * The occluding edge detail level, larger values provide more edges.

How to use 3d object finder node
-----------------------------------
.. video:: https://daoairoboticsinc-my.sharepoint.com/personal/xchen_daoai_com/_layouts/15/onedrive.aspx?ct=1644517096042&or=Teams%2DHL&id=%2Fpersonal%2Fxchen%5Fdaoai%5Fcom%2FDocuments%2FREAD%5FTHE%5FDOC%2F2%2E22%2E1%2F3d%5Fobj%5Ffinder%2Emp4&parent=%2Fpersonal%2Fxchen%5Fdaoai%5Fcom%2FDocuments%2FREAD%5FTHE%5FDOC%2F2%2E22%2E1
   :width: 100%

.. video:: https://daoairoboticsinc-my.sharepoint.com/personal/xchen_daoai_com/_layouts/15/onedrive.aspx?ct=1644517096042&or=Teams%2DHL&id=%2Fpersonal%2Fxchen%5Fdaoai%5Fcom%2FDocuments%2FREAD%5FTHE%5FDOC%2F2%2E22%2E1%2F3d%5Fobj%5Ffinder%5F2%2Emp4&parent=%2Fpersonal%2Fxchen%5Fdaoai%5Fcom%2FDocuments%2FREAD%5FTHE%5FDOC%2F2%2E22%2E1
   :width: 100%