Overview
==========================

Input 
--------------------

* Model mesh: a point cloud or mesh, used to align model to scene
* Scene cloud: a point cloud, represents the scene point cloud
* Hypothesis: a vector of poses, each pose represents a possible position of the model, the pose has to be relative close to ground truth in order to produce better result

Output
--------------------
* Poses: a vector of poses after the alignment

Parameters
---------------------

* Error Metric: Point-to-point is representative of the true error, while point-to-plane is representative of error relative to orientation. The change of relative pose that gives the minimal point-to-plane error is usually solved using standard nonlinear least-squares methods, which are often very slow. Generally, it is recommend using point to point error metric unless the geometry and amount of overlap between the hypothesis and scene are large to use the point to plane metric.
* Use Model box: Crops the scene based on the model's bounding box before alignment (speeds up matching)
* Max Iterations: Maximum iteration steps. The higher the number is, the longer it would take for alignment, but the alignment quality will be better with more iteration. Preset values are LOW=10 MEDIUM=50 HIGH=100
* True Error Tolerance: The error tolerance for coordination difference between the object and the scene. The alignment is more accurate when the tolerance is lower. Preset values are LOW=1 MEDIUM=5 HIGH=10
* Relative Error Tolerance: The error tolerance for orientation difference between the object and the scene. The alignment is more accurate when the tolerance is lower. Preset values are LOW=0.1 MEDUIM=1 HIGH=10
* Scene Decimation Step: Step size for sampling points in the scene. The larger the step size means the more points it will skip for the alignment algorithm. Generally, the smaller the step will result in more accuracy. Preset Values are LOW=15 MEDIUM=100 HIGH=500
* Model Decimation Step: Step size for sampling points in the model. This is similar to Scene Decimation Step.


