.. _aem_octree:

Create OcTree Mesh
==================

:ref:`OcTree meshes<octreeFile>` used in the AEM code are created using the program **AEMesh.exe**. This includes the inversion mesh (the global mesh on which the model lives) and a set of forward meshes (local OcTree meshes for each transmitter). Parameters necessary for creating all of the OcTree meshes are set in the :ref:`input file<aem_input_octree>`; referred to here as **octree_mesh.inp**.

To generate the OcTree meshes, open a command window. Type the path to the code **AEMesh.exe**, followed by a space, followed by the path to the input file.


**SYNTAX IMAGE NEEDED**


.. _aem_octree_output:


The program **octree_mesh_mt.exe** creates 5 output files:

    - **3D_mesh.txt:** the underlying regular :ref:`tensor mesh<tensorFile>` corresponding to the inversion mesh. This mesh is comprised of the smallest cell size and is very large (>> 1M cells). As a result, it is unwise to plot this mesh.

    - **3D_core_mesh.txt:** a 3D regular :ref:`tensor mesh<tensorFile>` defining the core region of the inversion mesh. 

    - **octree_mesh.txt:** the global inversion :ref:`OcTree mesh<octreeFile>`.

    - **active_cells_topo.txt:** an :ref:`active cells model<modelFile>` on the inversion mesh which defines the topography. Cells are active (underground) if assigned a value of 1 and inactive (in the air) if assigned a value of 0.

    - **octree_small_mesh.dat:** a binary data file containing the local forward meshes for all transmitters.

    - **AEMesh.log:** log file










