.. _elements:

Elements of the Program
=======================

This section provides a brief description of each program in the E3D version 2 package. In addition, we describe the file formats for all input and supporting files used by the coding library.

Program Library
---------------

The main executable programs within the E3D version 2 program library are:

    - **AEMesh:** creates a global OcTree mesh for the inversion based on the survey geometry and a set of local OcTree meshes about each transmitter and its receivers
    - **blk3cellOct:** creates a conductivity model on the OcTree mesh
    - **e3dinv_ver2:** single executable file for carrying out forward modeling and inversion of FEM data

Also included are the following Octree utility programs:

    - **extract_mesh:** extracts a specified local OcTree mesh from a hexidecimal file containing all local meshes
    - **create_weight_file:** creates cell weighting for the recovered model
    - **interface_weights:** creates weights on the faces of cells for the recovered model
    - **octree_cell_centre:** computes the cell centres of each octree cell
    - **octreeTo3D:** converts an OcTree model from its OcTree mesh to the underlying 3D base mesh
    - **refine_octree:** refine the octrees
    - **remesh_octree_model:** converts the octree model to base mesh


Main Input Files
----------------

Here, we describe the main input files for executables contained with the E3D version 2 package.

.. toctree::
    :maxdepth: 2

    Create octree mesh <inputfiles/createOcTree>
    Create octree model <inputfiles/createModel>
    Forward modeling <inputfiles/forward>
    Create face weights <inputfiles/weightsFiles>
    Inversion <inputfiles/inversion>


Supporting Files
----------------

Here, we describe the formats of supporting files used to run **e3dinv_ver2.exe**. The input files for each executable program are described in the :ref:`running the programs<running>` section.

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
    Model File <files/model>
    Model and Face Weights Files <files/weights>












