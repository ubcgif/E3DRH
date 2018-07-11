.. _running:

Running the programs
====================

This section provides describes how to run all executables pertaining to the E3DMT version 1 (2014 and 2015) package and the E3DMT version 2 (2017) package.

.. note::

    All executable files, input files, output filenames and files specified within input files can be specified in the following manner:

    - as just the filename if contained within the current working directory (Example: *filename.txt*)
    - as a file path relative to the current working directory (Example: *sub_dir\\filename.txt*)
    - as the full path (Example: *C:\\Users\\Name\\Tests\\filename.txt*)

    Executable files should **not** be renamed. However, input file names can be specified by the user if desired.

Version 1 (2014 and 2015)
-------------------------

.. important:: Although described here, this generation of the code may not be supported by GIFtools in the future.

Version 1 of the E3DMT codes make use of the following Fortran executables:

    - **e3dMTfwd:** Solves the forward problem. Computes the electric and magnetic response to a 3D conductivity model (fields, and impedance)
    - **e3dMTinv:** Solves the inverse problem using a direct solver approach (MUMPS). Recovers a conductivity model by inverting MT or ZTEM data. All entries of the impedance tensor or transfer function are needed.
    - **e3dMTinv_iter:** Solves the inverse problem using an iterative solver approach. Recovers a conductivity model by inverting MT or ZTEM data. All entries of the impedance tensor or transfer function are needed.
    - **MTcreate_octree_mesh_e3d:** Creates an octree mesh based on the :ref:`survey file<surveyFile>`
    - **blk3cell:** Creates models from a set of blocks on a tensor mesh
    - **3DModel2Octree:** Converts models from tensor to Octree meshes
    - **interface_weights:** Creates interface weights


Version 2 (2017)
----------------

Version 2 of the E3DMT code makes use of the following executables:

    - **e3dMTinv_ver2:** An all in one executable that can forward model or invert MT or ZTEM data
    - **octree_mesh_mt:** Creates an octree mesh based on the :ref:`receiver file<receiverFile>`
    - **blk3cellOct:** Creates models from a set of blocks directly on the octree mesh


Contents
--------

To learn the specifics of running each executable, see the following sections:

  .. toctree::
    :maxdepth: 1

    OcTree Mesh Generation <programs/createOcTree>
    Creating Octree Models <programs/createModel>
    Forward Modeling <programs/forward>
    Additional Cell and Face Weights <programs/weightsFiles>
    Inversion <programs/inversion>

