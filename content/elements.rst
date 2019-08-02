.. _elements:

Elements of the Program
=======================

This section provides a brief description of each program in the E3D version 2 tiled package. In addition, we describe the file formats for all input and supporting files used by the coding library.

Program Library
---------------

The main executable programs within the AEM program library are:

    - **e3d_v2_tiled:** Single executable file for carrying out forward modeling and inversion of FEM data
    - **create_octree_mesh_e3d_v2_tiled:** creates a global OcTree mesh for the inversion based on the survey geometry and a set of local OcTree meshes about each transmitter and its receivers

The following Octree utility programs are also used:

    - **blk3cellOct:** creates a conductivity model on the OcTree mesh
    - **extract_mesh:** extracts a specified local OcTree mesh from a hexidecimal file containing all local meshes
    - **create_weight_file:** creates cell weighting for the recovered model
    - **interface_weights:** creates weights on the faces of cells for the recovered model


Main Input Files
----------------

Here, we describe the main input files for executables contained with the E3D version 2 tiled package.

.. toctree::
    :maxdepth: 2

    Create octree mesh <inputfiles/createOcTree>
    Create octree model <inputfiles/createModel>
    Forward modeling <inputfiles/forward>
    Create face weights <inputfiles/weightsFiles>
    Inversion <inputfiles/inversion>


Supporting Files
----------------

Here, we describe the formats of supporting files used to run **e3d_v2_tiled.exe**. The input files for each executable program are described in the :ref:`running the programs<running>` section.

.. toctree::
    :maxdepth: 1

    Survey Index File <files/indexFile>
    Observations File <files/obsFile>
    Predicted Data File <files/preFile>
    Frequencies File <files/freqFile>
    Transmitter/Receiver File <files/receiverFile>
    Topography File <files/topoFile>
    Tensor Mesh File <files/tensor_mesh>
    Octree Mesh File <files/octree_mesh>
    Local Forward Meshes File <files/local_meshes>
    Active tiles file <files/active_tiles>
    Model File <files/model>
    Model and Face Weights Files <files/weights>
    












