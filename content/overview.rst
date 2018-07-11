.. _overview:

E3D package overview
====================

Description
-----------

This manual provides instruction and background for the e3d program library for the forward
modelling and inversion of frequency domain electromagnetic survey data. In order to decrease
computational time and increase accuracy by mesh refinement in areas of interest, e3d models
are discretized on an Octree mesh.  


.. figure:: images/OcTree.png
     :align: center
     :width: 700

     2D (QuadTree) mesh discretization about a ring (left). Cell refinement for OcTree mesh (right).


For ease of use the program library includes several utilities which generate a regular base mesh, enabling the user to construct initial or simulation models on
a regular mesh and then convert to an octree mesh. From the users point of view the software
operates in much the same way as previous GIF codes. This version is currently run through the
command line only.

The program library provides codes to do the following:

    - Construct models on a rectangular mesh, where each cell is assigned a constant value of conductivity, and transfers the model to an octree mesh.
    - Forward model electric and magnetic field anomaly responses to a 3D volume of contrasting conductivity, on and octree mesh.
    - Convert from and octree mesh to a regular base mesh.
    - Invert of surface, airborne, and/or borehole EM data to generate 3D conductivity models:

The inversion is solved as an optimization problem with the simultaneous goals of (i)
minimizing an objective function dependent on the model and (ii) generating synthetic
data that match observations to within a degree of misfit consistent with the statistics
of those data.

To counteract the inherent lack of information, the formulation incorporates reference
model and smoothing by regularization.

Capacity for the user to directionally weight smoothing and reference model influence
as well as overall influence of regulariztion on objective function minimization. Explicit
prior information may also take the form of upper and lower bounds on the conductivity
contrast in any cell.

he regularization parameter (controlling relative importance of objective function and
misfit terms). The initial research underlying this program library was funded principally by the mineral industry
consortium “Joint and Cooperative Inversion of Geophysical and Geological Data” (1991 -
1997) which was sponsored by NSERC and the following 11 companies: BHP Minerals, CRA Exploration,
Cominco Exploration, Falconbridge, Hudson Bay Exploration and Development, INCO
Exploration & Technical Services, Kennecott Exploration Company, Newmont Gold Company,
Noranda Exploration, Placer Dome, and WMC.


E3D Program Library Content
---------------------------

The main executable programs within the E3D program library are:

    - **create_octree_mesh_e3d:** creates an OcTree mesh based on the survey geometry
    - **e3dfwd_pardiso:** predicts data for a conductivity model
    - **e3dinv_pardiso:** inverts observed data to recover a conductivity model

Also included are the following Octree utility programs:

      - blk3cell
      - create_weight_file
      - interface_weights
      - octree_cell_centre
      - octreeTo3D
      - refine_octree
      - remesh_octree_model

Licensing
---------

A constrained educational version of the program is available with the `IAG <http://www.flintbox.com/public/project/1605/>`__ package
(please visit `UBC-GIF website <http://gif.eos.ubc.ca/>`__ for details). The educational version is fully functional so that users can learn
how to carry out effective and efficient 3D inversions of magnetic data. However, RESEARCH
OR COMMERCIAL USE IS NOT POSSIBLE because the educational version will
NOT work with more than 200 data points or 12,000 cells in the 3D mesh.

Licensing for an unconstrained academic version is available - see the `Licensing policy document <http://gif.eos.ubc.ca/software/licensing>`__.

NOTE: All academic licenses will be time-limited to one year. You can re-apply after that
time. This ensures that everyone is using the most recent versions of codes.

Licensing for commercial use is managed by distributors, not by the UBC-GIF research group.
Details are in the `Licensing policy document <http://gif.eos.ubc.ca/software/licensing>`__.


Installing E3D
--------------

There is no automatic installer currently available for the e3d. Please follow the following steps in
order to use the software:

    1. Extract all files provided from the given zip-based archive and place them all together in a new folder.
    2. Add this directory as new path to your environment variables.
    3. If you are running the software on a cluster of computers, please install the Message Pass Interface (MPI) on your computer and add it to your path in addition from
    4. Make sure to create a separate directory for each new inversion, where all the associated files will be stored. Do not store anything in the bin directory other than executable applications and Graphical User Interface applications (GUIs).

MPI can be downloaded `here <http://www.mcs.anl.gov/research/projects/mpich2/>`__ .




