.. _overview:

Package overview
================

.. important:: E3D version 2 tiled performs forward modeling and inversion with the executable **e3d_v2_tiled.exe**. Past iterations of this code may have been given the name 'AEM.exe', although its application is not limited to airborne. To use this code, ensure you have downloaded E3D version 2 'tiled' package from the UBC-GIF website.

Description
-----------

This manual provides instruction and background for the E3D version 2 tiled program library for the forward
modelling and inversion of frequency domain electromagnetic survey data. New to this
program is the ability to create many small local meshes on which to solve the EM forward problems
for each transmitter in parallel. The mesh generation code is parallelized with OpenMP and is meant to run on
a single node. It will use as many threads as available, or the user can use the **OMP_NUM_THREADS**
environment variable to indicate the number of threads.


.. figure:: images/OcTree.png
     :align: center
     :width: 700

     2D (QuadTree) mesh discretization about a ring (left). Cell refinement for OcTree mesh (right).


In order to decrease computational time and increase accuracy by mesh refinement in areas of interest, models
are discretized on an Octree mesh.
For ease of use the program library includes several utilities which generate a regular base mesh, enabling the user to construct initial or simulation models on
a regular mesh and then convert to an octree mesh. From the users point of view the software
operates in much the same way as previous GIF codes. This version is currently run through the
command line only.

The program library provides codes to do the following:

    - Construct models on a rectangular mesh, where each cell is assigned a constant value of conductivity, and transfers the model to an octree mesh.
    - Forward model magnetic field anomaly responses to a 3D volume of contrasting conductivity, on and octree mesh.
    - Convert from and octree mesh to a regular base mesh.
    - Invert of surface, airborne, and/or borehole EM data to generate 3D conductivity models:

The inversion is solved as an optimization problem with the simultaneous goals of (i)
minimizing an objective function dependent on the model and (ii) generating synthetic
data that match observations to within a degree of misfit consistent with the statistics
of those data.

To counteract the inherent lack of information, the formulation incorporates reference
model and smoothing by regularization.

Capacity for the user to directionally weight smoothing and reference model influence
as well as overall influence of regularization on objective function minimization. Explicit
prior information may also take the form of upper and lower bounds on the conductivity
contrast in any cell.

The regularization parameter (controlling relative importance of objective function and
misfit terms). The initial research underlying this program library was funded principally by the mineral industry
consortium “Joint and Cooperative Inversion of Geophysical and Geological Data” (1991 -
1997) which was sponsored by NSERC and the following 11 companies: BHP Minerals, CRA Exploration,
Cominco Exploration, Falconbridge, Hudson Bay Exploration and Development, INCO
Exploration & Technical Services, Kennecott Exploration Company, Newmont Gold Company,
Noranda Exploration, Placer Dome, and WMC.

In comparison with the E3D version 1 and 2 program libraries there are several new features for mesh generation and inversion. These include:

  - Surface and below surface topography cell size control. This allows the user to generate a mesh with refined cells near the surface of the topography to better capture features.

  - Small (tile) meshes are generated and focused around each source/receiver so that the forward problem can be split into many small problems and solved in parallel. The solutions are then interpolated back to the large base octree mesh. The user can specify the depth of each tile mesh, the number of cells surrounding source/receivers, and expand the polygon around the data.

  - A more versatile format for survey and observations files


Program Library Content
-----------------------

The main executable programs within the AEM program library are:

    - **e3d_v2_tiled:** Single executable file for carrying out forward modeling and inversion of FEM data
    - **create_octree_mesh_e3d_v2_tiled:** creates a global OcTree mesh for the inversion based on the survey geometry and a set of local OcTree meshes about each transmitter and its receivers

The following Octree utility programs are also used:

    - **blk3cellOct:** creates a conductivity model on the OcTree mesh
    - **extract_mesh:** extracts a specified local OcTree mesh from a hexidecimal file containing all local meshes
    - **create_weight_file:** creates cell weighting for the recovered model
    - **interface_weights:** creates weights on the faces of cells for the recovered model

Licensing
---------


Licensing for commercial use is managed by distributors, not by the UBC-GIF research group.
Details are in the `Licensing policy document <http://gif.eos.ubc.ca/software/licensing>`__.


Installing E3D
--------------

E3D Executables
^^^^^^^^^^^^^^^

There is no automatic installer currently available for the E3D program library. Please follow the following steps in
order to use the software:

    1. Extract all files provided from the given zip-based archive and place them all together in a new folder.
    2. Add this directory as new path to your environment variables.
    3. Make sure to create a separate directory for each new inversion, where all the associated files will be stored. Do not store anything in the bin directory other than executable applications and Graphical User Interface applications (GUIs).

MPI Executables
^^^^^^^^^^^^^^^

Message passaging interface (MPI) programming allows E3D version 2 tiled to utilize parallel computing. Even if the code is being run on a single machine, the user is **required** to download the necessary MPI package to use the executables. To set up MPI:

    1. Download and install:
      
      - `Microsoft MPI v10.0 <https://www.microsoft.com/en-us/download/details.aspx?id=57467>`__ : Required for window machines
      - `MPICH <https://www.mpich.org/downloads/>`__ : Required for Linux machines

    2. Path the folders containing MPI executables to your environment variables.


