.. _running:

.. important:: In the spring of 2022, a new suite of FDEM OcTree codes were compiled: *E3DRH, E3DRH v2 and E3DRH v2 tiled*. **These codes use a right-handed coordinate system**; as opposed to the modified left-handed coordinate system used by *E3D, E3D v2 and E3D v2 tiled*. **You are currently viewing the manual for the package which uses 'e3drh.exe' to forward model and invert FDEM data**. The manual for the original E3D v1 package (which uses 'e3d.exe') `can be found here <https://e3d.readthedocs.io/en/e3d/>`__ .

Running the programs
====================

This section provides describes how to run all executables pertaining to the E3DRH package.

.. note::

    All executable files, input files, output filenames and files specified within input files can be specified in the following manner:

    - as just the filename if contained within the current working directory (Example: *filename.txt*)
    - as a file path relative to the current working directory (Example: *sub_dir\\filename.txt*)
    - as the full path (Example: *C:\\Users\\Name\\Tests\\filename.txt*)

    Executable files should **not** be renamed. However, input file names can be specified by the user if desired.

The main executable programs within the E3DRH version 1 program library are:

    - **create_octree_mesh_e3d:** creates an OcTree mesh based on the survey geometry
    - **e3drh:** used to forward model or invert FEM data

The following Octree utility programs may also be helpful:

    - **blk3cell:** creates conductivity models on the underlying tensor mesh
    - **3DModel2Octree:** interpolates models from tensor to OcTree meshes
    - **create_weight_file:** creates the weighting on each cell in the model
    - **interface_weights:** creates weights on the faces of cells


**Contents:**

To learn the specifics of running each executable, see the following sections:

  .. toctree::
    :maxdepth: 1

    OcTree Mesh Generation <programs/createOcTree>
    Creating Octree Models <programs/createModel>
    Forward Modeling <programs/forward>
    Additional Cell and Face Weights <programs/weightsFiles>
    Inversion <programs/inversion>

