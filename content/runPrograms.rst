.. _running:

Running the programs
====================

This section provides describes how to run all executables pertaining to the AEM package.

.. note::

    All executable files, input files, output filenames and files specified within input files can be specified in the following manner:

    - as just the filename if contained within the current working directory (Example: *filename.txt*)
    - as a file path relative to the current working directory (Example: *sub_dir\\filename.txt*)
    - as the full path (Example: *C:\\Users\\Name\\Tests\\filename.txt*)

    Executable files should **not** be renamed. However, input file names can be specified by the user if desired.

The main executable programs within the AEM program library are:

    - **AEMesh:** creates a global OcTree mesh for the inversion based on the survey geometry and a set of local OcTree meshes about each transmitter and its receivers
    - **blk3cellOct:** creates a conductivity model on the OcTree mesh
    - **AEM:** Single executable file for carrying out forward modeling and inversion of FEM data

Also included are the following Octree utility programs:

    - **extract_mesh:** extracts a specified local OcTree mesh from a hexidecimal file containing all local meshes
    - **create_weight_file:** creates cell weighting for the recovered model
    - **interface_weights:** creates weights on the faces of cells for the recovered model
    - **octree_cell_centre:** computes the cell centres of each octree cell
    - **octreeTo3D:** converts an OcTree model from its OcTree mesh to the underlying 3D base mesh
    - **refine_octree:** refine the octrees
    - **remesh_octree_model:** converts the octree model to base mesh

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

