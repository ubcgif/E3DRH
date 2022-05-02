.. _elements:

.. important:: In the spring of 2022, a new suite of FDEM OcTree codes were compiled: *E3DRH, E3DRH v2 and E3DRH v2 tiled*. **These codes use a right-handed coordinate system**; as opposed to the modified left-handed coordinate system used by *E3D, E3D v2 and E3D v2 tiled*. **You are currently viewing the manual for the package which uses 'e3drh_v2.exe' to forward model and invert FDEM data**. The manual for the original E3D v2 package (which uses 'e3d_v2.exe') `can be found here <https://e3d.readthedocs.io/en/e3d_v2/>`__ .

Elements of the Program
=======================

This section provides a brief description of each program in the E3DRH version 2 package. In addition, we describe the file formats for all input and supporting files used by the coding library.

Program Library
---------------

The main executable programs within the E3DRH version 2 program library are:

    - **e3drh_v2:** single executable file for carrying out forward modeling and inversion of FEM data
    - **create_octree_mesh_e3d_v2:** creates a the OcTree mesh based on transmitter and receiver locations

The following Octree utility programs may also be helpful:

    - **blk3cellOct:** creates a conductivity model on the OcTree mesh
    - **create_weight_file:** creates cell weighting for the recovered model
    - **interface_weights:** creates weights on the faces of cells for the recovered model


Main Input Files
----------------

Here, we describe the main input files for executables contained with the E3DRH version 2 package.

.. toctree::
    :maxdepth: 1

    Create octree mesh <inputfiles/createOcTree>
    Create octree model <inputfiles/createModel>
    Forward modeling <inputfiles/forward>
    Create face weights <inputfiles/weightsFiles>
    Inversion <inputfiles/inversion>


Supporting Files
----------------

Here, we describe the formats of supporting files used to run **e3drh_v2.exe**. The input files for each executable program are described in the :ref:`running the programs<running>` section.

.. toctree::
    :maxdepth: 1

    Survey Index File <files/indexFile>
    Observations File <files/obsFile>
    Predicted Data File <files/preFile>
    Frequencies File <files/freqFile>
    Transmitter/Receiver File <files/receiverFile>
    Topography/Polygon File <files/topoFile>
    Tensor Mesh File <files/tensor_mesh>
    Octree Mesh File <files/octree_mesh>
    Model File <files/model>
    Model and Face Weights Files <files/weights>












