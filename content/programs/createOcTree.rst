.. _e3d_octree:

Create OcTree Mesh
==================

:ref:`OcTree meshes<octreeFile>` used in the E3D version 2 tiled code are created using the program **create_octree_mesh_e3d_v2_tiled.exe**. The program creates a global OcTree mesh (on which the model lives) and a set of local OcTree meshes (referred to as 'tiles') based on survey geometry. Parameters necessary for creating the OcTree meshes are set in the :ref:`input file<e3d_input_octree>`; referred to here as **octree_mesh.inp**.

To generate the OcTree meshes, open a command window. Type the path to the code **create_octree_mesh_e3d_v2_tiled.exe**, followed by a space, followed by the path to the input file.


.. figure:: images/run_create_octree.png
     :align: center
     :width: 500


.. _e3d_octree_output:


The program **create_octree_mesh_e3d_v2_tiled.exe** creates 5 output files:

    - **3D_mesh.txt:** the underlying regular :ref:`tensor mesh<tensorFile>` corresponding to the global OcTree mesh. This mesh is comprised of the smallest cell size and is very large (>> 1M cells). As a result, it is unwise to plot this mesh.

    - **3D_core_mesh.txt:** a 3D regular :ref:`tensor mesh<tensorFile>` defining the core region of the global OcTree mesh. 

    - **octree_mesh.txt:** the global :ref:`OcTree mesh<octreeFile>`.

    - **active_cells_topo.txt:** an :ref:`active cells model<modelFile>` on the global OcTree mesh which defines the topography. Cells are active (underground) if assigned a value of 1 and inactive (in the air) if assigned a value of 0.

    - **octree_small_mesh.dat:** a binary data file containing the local forward meshes for all transmitters.

    - **AEMesh.log:** log file










