Overview
------------------------

Input 
~~~~~~~~~~~~~~~~~~~~~~~~~~~
Scene cloud: one or a vector of point clouds to find objects within.

Output
~~~~~~~~~~~~~~~~~~~~~~~~~~~

* cloudModel: active model used for searching, represented as point cloud
* edgesModel: active model used for searching, represented as edge cloud. Available only in edge mode
* msehModel: active model used for searching, represented as mesh. Available only when the model is defined by mesh
* resultPoses: a vector of pose representing the result of search
* success: a field indicating whether the search is successful (at least one position found)


