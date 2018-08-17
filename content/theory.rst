.. _theory:

Background Theory
=================

This section aims to provide the user with a basic review of the physics, discretization, and optimization
techniques used to solve the frequency domain electromagnetics problem. It is assumed
that the user has some background in these areas. For further reading see (Nabighian 2006) (**cite**).

.. _theory_fundamentals:

Fundamental Physics
-------------------

Maxwell's equations provide the starting point from which an understanding of how electromagnetic
fields can be used to uncover the substructure of the Earth. In the frequency domain Maxwell's
equations are:

.. math::
    \begin{align}
        \nabla \times &\mathbf{E} + i\omega\mu \mathbf{H} = 0 \\
        \nabla \times &\mathbf{H} - \sigma \mathbf{E} = \mathbf{S} \\
        &\mathbf{\hat{n} \times H} = 0
    \end{align}
    :label: maxwells_eq

where :math:`\mathbf{E}` and :math:`\mathbf{H}` are the electric and magnetic fields, :math:`\mathbf{S}` is some external source and :math:`e^{+i\omega t}` is suppressed.
Symbols :math:`\mu`, :math:`\sigma` and :math:`\omega` are the magnetic permeability, conductivity, and angular frequency, respectively. This formulation assumes a quasi-static mode so that the system can be viewed as a diffusion equation (Weaver, 1994; Ward and Hohmann, 1988 in :cite:`Nabighian1991`). By doing so, some difficulties arise when
solving the system;

    - the curl operator has a non-trivial null space making the resulting linear system highly ill-conditioned
    - the conductivity :math:`\sigma` varies over several orders of magnitude
    - the fields can vary significantly near the sources, but smooth out at distance thus high resolution is required near sources

These issues are addressed by considering a Helmholz potential formulation to deal with the null
space of the curl operator, harmonic averaging and mesh refinement to combat large jumps in
conductivities, and the ability to refine the mesh near the sources to improve resolution.



Octree Mesh
-----------

By using an Octree discretization of the earth domain, the areas near sources and likely model
location can be give a higher resolution while cells grow large at distance. In this manner, the
necessary refinement can be obtained without added computational expense. Figure(2) shows an
example of an Octree mesh, with nine cells, eight of which are the base mesh minimum size.


.. figure:: images/OcTree.png
     :align: center
     :width: 700


When working with Octree meshes, the underlying mesh is defined as a regular 3D orthogonal grid where
the number of cells in each dimension are :math:`2^{m_1} \times 2^{m_2} \times 2^{m_3}`, with grid size :math:`h`. This underlying mesh
is the finest possible, so that larger cells have lengths which increase by powers of 2 multiplied by
:math:`h`. The idea is that if the recovered model properties change slowly over a certain volume, the cells
bounded by this volume can be merged into one without losing the accuracy in modeling, and are
only refined when the model begins to change rapidly.



Discretization of Operators
---------------------------

The operators div, grad, and curl are discretized using a finite volume formulation. Although div and grad do not appear in :eq:`maxwells_eq`, they are required for the solution of the system. The divergence operator is discretized in the usual flux-balance approach, which by Gauss' theorem considers the current flux through each face of a cell. The nodal gradient (operates on a function with values on the nodes) is obtained by differencing adjacent nodes and dividing by edge length. The discretization of the curl operator is computed similarly to the divergence operator by utilizing Stokes theorem by summing the magnetic field components around the edge of each face. Please
see :cite:`Haber2012` for a detailed description of the discretization process.


Forward Problem
---------------

The solution for the fields :math:`\mathbf{H} and :math:`\mathbf{E} can either be computed iteratively or directly depending on
the number of sources. If the number of sources is small than an iterative method (BiCGstab) is
used. Because of the null space of the curl operator a discrete Helmholz decomposition is used to
write the electric field as:

.. math::
    \mathbf{E} = \mathbf{A} + \nabla \phi


The problem is then solved by eliminating the curl operator and solving for :math:`\mathbf{A}` and :math:`\phi`.
If on the other hand if there are many sources, it is more efficient to directly decompose the
forward matrix system by LU factorization. By doing so, many systems can be solved with a single
factorization. MUMPS (Amestoy et al. (2001)) is used for the factorization and can be downloaded
`here <http://graal.ens-lyon.fr/MUMPS/>`__.

The forward problem of simulating data can now be written in the following form. Let :math:`\mathbf{A(m)}` be
the discrete linear system obtained by the discretiztion of Maxwell’s equations, where :math:`\mathbf{m} = log (\boldsymbol{\sigma})`.

Assuming there are :math:`n_s` sources :math:`\mathbf{S} = i\omega(\mathbf{s_1, s_2, ....., s_{n_2}})` and that :math:`\mathbf{P^T}` is a projection from edges to receivers then the simulated EM field data can be written as:

.. math::
    \mathbb{F}[\mathbf{m}] = \mathbf{P^T A(m)^{-1} \, S}



.. _theory_inv:

Inverse Problem
---------------

Solving the non-linear EM inverse problem for electric conductivity is akin to minimizing the
following objective function

.. math::
    \Phi_d (\mathbf{m}) = \frac{1}{2} \big \| \mathbf{W_d} \big ( \mathbb{F}[\mathbf{m}] - \mathbf{d^{obs}} \big ) \big \|^2

where :math:`\mathbf{d^{obs}}` is the observed data, :math:`\mathbb{F}[\mathbf{m}]` is the predicted data for the current model and :math:`\mathbf{W_d}` is a diagonal matrix consisting of the reciprocal of the uncertainties on the data. Due to the ill-posedness of the problem, there are no stable solutions and a regularization is needed. The
regularization used penalizes for both smoothness, and likeness to a reference model :math:`\mathbf{m_{ref}}` supplied by the user

.. math::
    \Phi_m (\mathbf{m - m_{ref}}) = \frac{1}{2} \big \| \nabla (\mathbf{m - m_{ref}}) \big \|^2


An important consideration comes when discretizing the regularization. The gradient operates on
cell centered variables in this instance. Applying a short distance approximation is second order
accurate on a domain with uniform cells, but only O(1) on areas where cells are non-uniform. To
rectify this a higher order approximation is used Haber et al. (2012). The discrete regularization
operator can then be expressed as

.. math::
    \Phi_m (\mathbf{m}) = \frac{1}{2} \int | \nabla m |^2 \, dV \approx \frac{1}{2}\alpha \mathbf{m^T G_c^T} \textrm{diag} \big ( \mathbf{A_f^T v} \big ) \mathbf{G_c \, m}


where :math:`\mathbf{A_f}` is an averaging matrix from faces to cell centres, :math:`\mathbf{G_c}` is the cell centre to cell face gradient
operator, and :math:`\mathbf{v}` is the cell volume For the benefit of the user, let :math:`\mathbf{R^T R}` be the weighting matrix given by

.. math::
    \mathbf{R^T R} = \alpha \mathbf{G_c^T} \textrm{diag} \big ( \mathbf{A_f^T v} \big ) \mathbf{G_c}

which can be also be written as

.. math::
    \mathbf{R^T R} = \begin{bmatrix} \alpha_x & & \\ & \alpha_y & \\ & & \alpha_z \end{bmatrix}
    \begin{bmatrix} \mathbf{G_x^T} & \mathbf{G_y^T} & \mathbf{G_z^T} \end{bmatrix} \textrm{diag} \big ( \mathbf{A_f^T v} \big )
    \begin{bmatrix} \mathbf{G_x^T} \\ \mathbf{G_y^T} \\ \mathbf{G_z^T} \end{bmatrix}



In the code the :math:`\mathbf{R^T R}` matrix is stored as a separate matrix so that individual model norm components
can be calculated.

The resulting optimization problem is then

.. math::
    \begin{align}
    &\min_{\mathbf{m}} \;\; \Phi_d (\mathbf{m}) + \beta \Phi_m ( \mathbf{m - m_{ref}}) \\ 
    &s.t. \;\; \mathbf{m_L} \preceq \mathbf{m} \preceq \mathbf{m_H}
    \end{align}

where :math:`\beta` is trade-off parameter for the regularization, and :math:`\mathbf{m_L}` and :math:`\mathbf{m_H}` are upper and lower bounds provided by
some a prior geological information.
A simple Gauss-Newton optimization method is used to where the system of equations is solved
using ipcg (incomplete preconditioned conjugate gradients) to solve for each G-N step. For more
information refer again to Haber et al. (2012) and references therein.



Cell Weighting
^^^^^^^^^^^^^^

Now, if a cell weighting is used it is applied to the entire norm, that
is, there is a :math:`w_i` for each cell

.. math:: 
    \mathbf{\tilde{R}^T \tilde{R}} = \alpha \mathbf{W^T \, G_c^T} \textrm{diag} \big ( \mathbf{A_f^T v} \big ) \mathbf{W \, G_c}


where :math:`\mathbf{W}` contains the additional weights. 
There is also the option of choosing a cell interface weighting. This allows for a weight on each cell
FACE. The user must supply the weights (:math:`w_x, w_y, w_z`) for each weighted cell.
When the interface weighting option is chosen and the value is less than 1, a sharp discontinuity will be created.
When the value is greater than 1, there will be a smooth transition. To prevent the inversion from putting
”junk” on the surface, the top X and Y face weights should have a large value

.. math::
    \mathbf{\tilde{R}^T \tilde{R}} = \alpha_x \mathbf{G_x^T} \textrm{diag} \big ( \mathbf{W_x A_f^T v} \big ) \mathbf{G_x}
    + \alpha_y \mathbf{G_y^T} \textrm{diag} \big ( \mathbf{W_y A_f^T v} \big ) \mathbf{G_y}
    + \alpha_z \mathbf{G_z^T} \textrm{diag} \big ( \mathbf{W_z A_f^T v} \big ) \mathbf{G_z}


Sparse Norms
^^^^^^^^^^^^

The Ekblom regulization allows the user to essentially change the norm or distance measure of the regulization. The discrete Ekblom norm is given by

.. math::
    \phi_E = \mathbf{V^T} \big [ \mathbf{A_f} \big [ \mathbf{G} [\mathbf{m - m_{ref}} ] \big ]^2 + \epsilon \big ]^p


where :math:`\mathbf{G}` is the gradient operator. And as a result:

.. math::
    \mathbf{R^T R} = \mathbf{G^T} \textrm{diag} \Big ( \mathbf{A_f^T v} \big [ \mathbf{A_f} [\mathbf{G} (\mathbf{m - m_{ref}}) ] \big ]^2 + \epsilon \big ]^{p-1} \Big ) \mathbf{G}


The Ekblom norm can be controlled by the user by choosing the parameters :math:`p` and :math:`\epsilon`.





