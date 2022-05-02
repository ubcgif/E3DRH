.. _overview:

.. important:: In the spring of 2022, a new suite of FDEM OcTree codes were compiled: *E3DRH, E3DRH v2 and E3DRH v2 tiled*. **These codes use a right-handed coordinate system**; as opposed to the modified left-handed coordinate system used by *E3D, E3D v2 and E3D v2 tiled*. **You are currently viewing the manual for the package which uses 'e3drh.exe' to forward model and invert FDEM data**. The manual for the original E3D v1 package (which uses 'e3d.exe') `can be found here <https://e3d.readthedocs.io/en/e3d/>`__ .

Package overview
================

Description
-----------

This manual provides instruction and background for the **E3DRH version 1** program library for the forward
modelling and inversion of frequency domain electromagnetic survey data in a right-handed coordinate system.
In order to decrease computational time and increase accuracy by mesh refinement in areas of interest, conductivity models
are discretized on an Octree mesh.  


.. figure:: images/OcTree.png
     :align: center
     :width: 700

     2D (QuadTree) mesh discretization about a ring (left). Cell refinement for OcTree mesh (right).


For ease of use the program library includes several utilities which generate OcTree meshes and additional weights. From the users point of view the software
operates in much the same way as previous GIF codes. This version is currently run through the
command line only.

The program library provides codes to do the following:

    - Construct models on OcTree meshes.
    - Forward model electric and magnetic field anomaly responses to a 3D volume of contrasting conductivity, on and octree mesh.
    - Invert of surface, airborne, and/or borehole EM data to recover 3D conductivity models:

The inversion is solved as an optimization problem with the simultaneous goals of (i)
minimizing an objective function dependent on the model and (ii) generating synthetic
data that match observations to within a degree of misfit consistent with the statistics
of those data.

To counteract the inherent lack of information, the formulation incorporates reference
model and regularization.

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


Program Library Content
-----------------------

The main executable programs within the E3DRH version 1 program library are:

    - **create_octree_mesh_e3d:** creates an OcTree mesh based on the survey geometry
    - **e3drh:** used to forward model and inverted FEM data

The following Octree utility programs may also be helpful:

    - **blk3cell:** creates conductivity models on the underlying tensor mesh
    - **3DModel2Octree:** interpolates models from tensor to OcTree meshes
    - **create_weight_file:** creates the weighting on each cell in the model
    - **interface_weights:** creates weights on the faces of cells

Licensing
---------

Licensing for commercial use is managed by distributors, not by the UBC-GIF research group.
Details are in the `Licensing policy document <http://gif.eos.ubc.ca/software/licensing>`__.


Installing E3DRH
----------------

E3DRH Executables
^^^^^^^^^^^^^^^^^

There is no automatic installer currently available for E3DRH version 1. Please follow the following steps in
order to use the software:

    1. Extract all files provided from the given zip-based archive and place them all together in a new folder.
    2. Add this directory as new path to your environment variables.
    3. Make sure to create a separate directory for each new inversion, where all the associated files will be stored. Do not store anything in the bin directory other than executable applications and Graphical User Interface applications (GUIs).

MPI Executables
^^^^^^^^^^^^^^^

Message passaging interface (MPI) programming allows E3DRH version 1 to utilize parallel computing. Even if the code is being run on a single machine, the user is **required** to download the necessary MPI package to use the E3DRH version 1 executables. To set up MPI:

    1. Download and install:
      
      - `Microsoft MPI v10.0 <https://www.microsoft.com/en-us/download/details.aspx?id=57467>`__ : Required for window machines
      - `MPICH <https://www.mpich.org/downloads/>`__ : Required for Linux machines

    2. Path the folders containing MPI executables to your environment variables.



