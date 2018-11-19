.. _e3d_octree:

Create OcTree Mesh
==================

:ref:`OcTree meshes<octreeFile>` used in the E3D version 2 code are created using the program **create_mesh_newformat_e3d.exe**. Parameters necessary for creating the OcTree meshes are set in the :ref:`input file<e3d_input_octree>`; referred to here as **create_octree.inp**.

To generate the OcTree meshes, open a command window. Type the path to the code **create_mesh_newformat_e3d.exe**, followed by a space, followed by the path to the input file.


.. figure:: images/run_create_octree.png
     :align: center
     :width: 500


.. _e3d_octree_output:


The program **create_mesh_newformat_e3d.exe** creates 5 output files:

    - **3D_mesh.txt:** the underlying :ref:`tensor mesh<tensorFile>` for the OcTree mesh. This mesh is comprised of the smallest cell size and is very large (>> 1M cells). As a result, it is unwise to plot this mesh.

    - **3D_core_mesh.txt:** a 3D :ref:`tensor mesh<tensorFile>` defining the core region of the OcTree mesh. 

    - **octree_mesh.txt:** the :ref:`OcTree mesh<octreeFile>`.

    - **active_cells_topo.txt:** an :ref:`active cells model<modelFile>` which defines the topography on the OcTree mesh. Cells are active (underground) if assigned a value of 1 and inactive (in the air) if assigned a value of 0.

    - **E3DMesh.log:** log file










