.. _elements:

Elements of the Program E3D
===========================

This section provides a brief description of each program in the E3D package. In addition, we describe the file formats for all input and supporting files used by the coding library.

Program Library
---------------

The main executable programs within the E3D program library are:

    - **create_octree_mesh_e3d:** creates an OcTree mesh based on the survey geometry
    - **e3dfwd_pardiso:** predicts data for a conductivity model
    - **e3dinv_pardiso:** inverts observed data to recover a conductivity model

Also included are the following Octree utility programs:

    - **blk3cell:** creates conductivity on underlying tensor
    - **create_weight_file:** creates the weighting on each cell in the model
    - **interface_weights:** creates weights on the faces of cells
    - **octree_cell_centre:** computes the cell centres of each octree cell
    - **octreeTo3D:** converts and octree mesh to a 3D base mesh
    - **refine_octree:** refine the octrees
    - **remesh_octree_model:** converts the octree model to base mesh


Main Input Files
----------------

Here, we describe the main input files for executables contained with the E3DMT version 1 and version 2 coding packages.

.. toctree::
    :maxdepth: 2

    Create octree mesh <inputfiles/createOcTree>
    Create octree model <inputfiles/createModel>
    Forward modeling <inputfiles/forward>
    Create face weights <inputfiles/weightsFiles>
    Inversion <inputfiles/inversion>


Supporting Files
----------------

Here, we describe the formats of supporting files used to run E3DMT executable files. The input files for each executable program are described in the :ref:`running the programs<running>` section.

.. toctree::
    :maxdepth: 1

    Survey and Locations File <files/surveyFile>
    Receiver File <files/receiverFile>
    Survey Index File <files/indexFile>
    Frequencies Files <files/freqFile>
    Predicted Data File <files/preFile>
    Observations File <files/obsFile>
    Topography File <files/topoFile>
    Tensor Mesh File <files/tensor_mesh>
    Octree Mesh File <files/octree_mesh>
    Model File <files/model>
    Model and Face Weights Files <files/weights>












