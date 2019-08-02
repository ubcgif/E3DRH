.. _running:

Running the programs
====================

This section provides describes how to run all executables pertaining to the E3D version 2 package.

.. note::

    All executable files, input files, output filenames and files specified within input files can be specified in the following manner:

    - as just the filename if contained within the current working directory (Example: *filename.txt*)
    - as a file path relative to the current working directory (Example: *sub_dir\\filename.txt*)
    - as the full path (Example: *C:\\Users\\Name\\Tests\\filename.txt*)

    Executable files should **not** be renamed. However, input file names can be specified by the user if desired.

The main executable programs within the E3D version 2 program library are:

    - **e3d_v2:** single executable file for carrying out forward modeling and inversion of FEM data
    - **create_octree_mesh_e3d_v2:** creates a the OcTree mesh based on transmitter and receiver locations

The following Octree utility programs may also be helpful:

    - **blk3cellOct:** creates a conductivity model on the OcTree mesh
    - **create_weight_file:** creates cell weighting for the recovered model
    - **interface_weights:** creates weights on the faces of cells for the recovered model

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

