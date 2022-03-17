Alignment Node
=================

The Alignment Node uses an iterative algorithm to refine poses for better alignment.
Given initial poses, an input model mesh is iteratively aligned toward an input scene cloud by sampling points, matching them between the model and scene,
and minimizing the error between matched points.
This node should be used when reasonably accurate poses have already been obtained, such as following after the Scene Match Node or Mod Finder Node, 
in which case these poses can be further refined.

The alignment node usually follow after a node provides model mesh input(reader, mesh process node), 
a node provides scene cloud(camera, cloud process node), and a node provides a reasonably good match for further alignment(3d object finder node).

.. toctree::
   :maxdepth: 1

   alignment_overview
   alignment_procedure
   