.. _elements:

Elements of the Program E3DMT
=============================

This section provides a brief description of each program in the E3DMT version 1 and version 2 libraries. In addition, we describe the file formats for all input and supporting files used by these coding libraries.

Version 1 (2014 and 2015)
-------------------------

.. important:: Although described here, this generation of the code may not be supported by GIFtools in the future.

Version 1 of the E3DMT codes makes use of the following executables:

    - **e3dMTfwd:** Solves the forward problem. Computes the electric and magnetic response to a 3D conductivity model (fields, and impedance)
    - **e3dMTinv:** Solves the inverse problem using a direct solver approach (MUMPS). Recovers a conductivity model by inverting MT or ZTEM data. All entries of the impedance tensor or transfer function are needed.
    - **e3dMTinv_iter:** Solves the inverse problem using an iterative solver approach. Recovers a conductivity model by inverting MT or ZTEM data. All entries of the impedance tensor or transfer function are needed.
    - **MTcreate_octree_mesh_e3d:** Creates an octree mesh based on the :ref:`survey file<surveyFile>`
    - **blk3cell:** Creates models from a set of blocks on a tensor mesh
    - **3DModel2Octree:** Converts models from tensor to Octree meshes
    - **interface_weights:** Creates interface weights

Version 2 (2017)
----------------

.. important:: This generation of the E3DMT code is meant to be maintained longterm.

Version 2 of the E3DMT code makes use of the following executables:

    - **e3dMTinv_ver2:** An all in one executable that can forward model or invert MT or ZTEM data
    - **octree_mesh_mt:** Creates an octree mesh based on the :ref:`receiver file<receiverFile>`
    - **blk3cellOct:** Creates models from a set of blocks directly on the octree mesh

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












