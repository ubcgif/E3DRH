.. _elements:

.. important:: In the spring of 2022, a new suite of FDEM OcTree codes were compiled: *E3DRH, E3DRH v2 and E3DRH v2 tiled*. **These codes use a right-handed coordinate system**; as opposed to the modified left-handed coordinate system used by *E3D, E3D v2 and E3D v2 tiled*. **You are currently viewing the manual for the package which uses 'e3drh.exe' to forward model and invert FDEM data**. The manual for the original E3D v1 package (which uses 'e3d.exe') `can be found here <https://e3d.readthedocs.io/en/e3d/>`__ .

Elements of the E3DRH version 1 package
=======================================

This section provides a brief description of each program in the E3DRH version 1 package. In addition, we describe the file formats for all input and supporting files used by the coding library.

Program Library
---------------

The main executable programs within the E3DRH version 1 program library are:

    - **create_octree_mesh_e3d:** creates an OcTree mesh based on the survey geometry
    - **e3drh:** used to forward model or invert FEM data

The following Octree utility programs may also be helpful:

    - **blk3cell:** creates conductivity models on the underlying tensor mesh
    - **3DModel2Octree:** interpolates models from tensor to OcTree meshes
    - **create_weight_file:** creates the weighting on each cell in the model
    - **interface_weights:** creates weights on the faces of cells

Main Input Files
----------------

Here, we describe the main input files for executables contained with the E3DRH version 1 coding package.

.. tOcTree::
    :maxdepth: 1

    Create OcTree mesh <inputfiles/createOcTree>
    Create OcTree model <inputfiles/createModel>
    Forward modeling <inputfiles/forward>
    Create face weights <inputfiles/weightsFiles>
    Inversion <inputfiles/inversion>


Supporting Files
----------------

Here, we describe the formats of supporting files used to run E3DRH executable files. The input files for each executable program are described in the :ref:`running the programs<running>` section.

.. toctree::
    :maxdepth: 1

    Survey and Locations File <files/surveyFile>
    Predicted Data File <files/preFile>
    Observations File <files/obsFile>
    Topography File <files/topoFile>
    Tensor Mesh File <files/tensor_mesh>
    OcTree Mesh File <files/octree_mesh>
    Model File <files/model>
    Model and Face Weights Files <files/weights>












