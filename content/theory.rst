.. _theory:

Background Theory
=================

This section aims to provide the user with a basic review of the physics, discretization, and optimization techniques used to solve the frequency domain quasi-static electromagnetics problem. It
is assumed that the user has some background in these areas. For further reading see :cite:`Nabighian1991`.

.. _theory_fundamentals:

Fundamental Physics
-------------------

Maxwell's equations provide the starting point from which an understanding of how electromagnetic
fields can be used to uncover the substructure of the Earth. In the frequency domain Maxwell's
equations are:

.. math::
    \begin{align}
        \nabla \times &\mathbf{E} - i\omega\mu \mathbf{H} = 0 \\
        \nabla \times &\mathbf{H} - \sigma \mathbf{E} = \mathbf{S} 
    \end{align}
    :label:

where :math:`\mathbf{E}` and :math:`\mathbf{H}` are the electric and magnetic fields, :math:`\mathbf{S}` is some external source and :math:`e^{-i\omega t}` is suppressed. Symbols :math:`\mu`, :math:`\sigma` and :math:`\omega` are the magnetic permeability, conductivity, and angular frequency, respectively. This formulation assumes a quasi-static mode so that the system can be viewed as a diffusion equation (Weaver, 1994; Ward and Hohmann, 1988 in :cite:`Nabighian1991`). By doing so, some difficulties arise when
solving the system;

    - the curl operator has a non-trivial null space making the resulting linear system highly ill-conditioned
    - the conductivity :math:`\sigma` varies over several orders of magnitude

.. _theory_nsem:

Natural Sources: MT and ZTEM
----------------------------

The sources in the magnetotelluric (MT) and Z-axis tipper elecromagnetic (ZTEM) methods are modeled as plain waves originating
from natural phenomenon. These waves can be of very low frequency (< 1 Hz) and very high
energy, making it possible to image very deep targets. This also implies that the source term is
zero inside the domain of interest, and therefore the source term on the boundaries becomes very
important. For natural source electromagnetic (NSEM) problems, we solve the following system:

.. math::
    \begin{align}
        \nabla \times &\mathbf{E} - i\omega\mu \mathbf{H} = 0 \\
        \nabla \times &\mathbf{H} - \sigma \mathbf{E} = 0 \\
        &\mathbf{E} \big |_{\partial \Omega} = \mathbf{E_0}
    \end{align}
    :label: NSEM_system

where :math:`\mathbf{E_0}` is the electric field solution on the boundary :math:`\partial \Omega`.

Consider the case where the Earth is a uniform half-space with a plane surface. If the source field is assumed
to be homogeneous, infinite in dimension, and is located at infinity, then the plane waves impinging on the Earth's surface travel in the z-direction.

For plane waves polarized such that their electric fields lie along the x direction, the electric field is defined by the following Helmholtz equation:

.. math::
    \frac{\partial^2 E_x}{\partial z^2} = k^2 E_x \;\;\; \textrm{s.t.} \;\;\; k^2 = -i\mu\omega\sigma
    :label: Helmholtz_E

and the relationship between :math:`E_x` and :math:`H_y` is given by:

.. math::
    i \omega \mu H_y = \frac{\partial E_x}{\partial z}
    :label:

The solution to :eq:`Helmholtz_E` takes the form:

.. math::
    E_x = Q e^{-kz}
    :label:

where :math:`Q` is some constant. Taking the ratio of the electric and magnetic fields measured at the surface
gives:

.. math::
    Z = \frac{E_x}{H_y} = \frac{-i\omega \mu}{k} = \sqrt{\dfrac{-i\omega\mu}{\sigma}}
    :label: impedance_hs


This implies that conductivity :math:`\sigma` of the Earth can be determined by taking measurements of the
field components, and therefore the impedance constitutes the basic MT response function, or data.
A 1D layered Earth model can be used to compute the source wave components by iteratively propagating a plane wave from the surface to depth.

.. For -iwt formulation. Theory verified up to here.

Magnetotelluric (MT) Data
^^^^^^^^^^^^^^^^^^^^^^^^^

For a 3-dimensional Earth, the magnetotelluric data are defined by the impedance tensor. The impedance tensor can be defined using the ratios of electric and magnetic field components in both the x and y directions for 2 orthogonal plane wave polarizations; one polarization with the electric field along the x axis and one polarization with the electric file along the y axis. Where the impedance tensor :math:`\mathbf{Z}` is a 2 by 2 matrix:

.. math::
    \mathbf{Z} = \mathbf{E H}^{-1}
    :label:

such that:

.. math::
    \begin{bmatrix} Z_{xx} & Z_{xy} \\ Z_{yx} & Z_{yy} \end{bmatrix} =
    \begin{bmatrix} E_{x}^{(1)} & E_{x}^{(2)} \\ E_{y}^{(1)} & E_{y}^{(2)} \end{bmatrix}
    \begin{bmatrix} H_{x}^{(1)} & H_{x}^{(2)} \\ H_{y}^{(1)} & H_{y}^{(2)} \end{bmatrix}^{-1}
    :label: impedance_tensor

where 1 and 2 refer to fields associated with plane waves polarized along two perpendicular directions.



ZTEM Data
^^^^^^^^^

The Z-Axis Tipper Electromagnetic Technique (ZTEM) (Lo2008) records
the vertical component of the magnetic field everywhere above the survey area while recording
the horizontal fields at a ground base reference station. In the same manner as demonstrated for
MT, transfer functions are computed which relate the vertical fields to the ground based horizontal
fields. This relation is given by:

.. math::
    H_z(r) = T_{zx}(r,r_0)H_x(r_0) + T_{zy}(r,r_0)H_y(r_0)
    :label:

where :math:`r` is the location of the vertical field and :math:`r_0` is the location of the ground base station. :math:`T_{zx}` and :math:`T_{zy}` are the vertical field transfer functions, from z to x and z to y respectively. For a 3-dimensional Earth, the transfer function can be defined using the magnetic field components for 2 orthogonal plane wave polarizations; one polarization with the electric field along the x axis and one polarization with the electric file along the y axis. In this case,

.. math::
    \begin{bmatrix} H_z^{(1)} \\ H_z^{(2)} \end{bmatrix} =
    \begin{bmatrix} H_x^{(1)} & H_y^{(1)} \\ H_x^{(2)} & H_y^{(2)} \end{bmatrix}
    \begin{bmatrix} T_{zx} \\ T_{zy} \end{bmatrix}
    :label: transfer_fcn

where 1 and 2 refer to fields associated with plane waves polarized along two perpendicular directions. Thus the transfer functions are given by:

.. math::
    \begin{bmatrix} T_{zx} \\ T_{zy} \end{bmatrix} = \big ( H_x^{(1)} H_y^{(2)} - H_x^{(2)} H_y^{(1)} \big )^{-1}
    \begin{bmatrix} - H_y^{(1)} H_z^{(2)} + H_y^{(2)} H_z^{(1)} \\ H_x^{(1)} H_z^{(2)} - H_x^{(2)} H_z^{(1)} \end{bmatrix}
    


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

The operators div, grad, and curl are discretized using a finite volume formulation. Although div and grad do not appear in :eq:`impedance_tensor`, they are required for the solution of the system. The divergence
operator is discretized in the usual flux-balance approach, which by Gauss' theorem considers the current flux through each face of a cell. The nodal gradient (operates on a function with values on the nodes) is obtained by differencing adjacent nodes and dividing by edge length. The discretization of the curl operator is computed similarly to the divergence operator by utilizing Stokes theorem by summing the magnetic field components around the edge of each face. Please
see :cite:`Haber2012` for a detailed description of the discretization process.


Forward Problem
---------------

To solve the forward problem, we must first discretize and solve for the fields in Eq. :eq:`NSEM_system`, where :math:`e^{-i\omega t}` is suppressed. Using finite volume discretization, the electric fields on cell edges (:math:`\mathbf{u_e}`) are obtained by solving the following system at every frequency:

.. math::
    \big [ \mathbf{C^T \, M_\mu \, C} + i\omega \mathbf{M_\sigma} \big ] \, \mathbf{u_e} = \mathbf{s}
    :label: discrete_e_sys

where :math:`\mathbf{C}` is the curl operator and:

.. math::
    \begin{align}
    \mathbf{M_\mu} &= diag \big ( \mathbf{A^T_{f2c} V} \, \boldsymbol{\mu^{-1}} \big ) \\
    \mathbf{M_\sigma} &= diag \big ( \mathbf{A^T_{e2c} V} \, \boldsymbol{\sigma} \big ) \\
    \end{align}

where :math:`\mathbf{V}` is a diagonal matrix containing  all cell volumes, :math:`\mathbf{A_{f2c}}` averages from faces to cell centres and :math:`\mathbf{A_{e2c}}` averages from edges to cell centres. The magnetic permeabilities and conductivities for each cell are contained within vectors :math:`\boldsymbol{\mu}` and :math:`\boldsymbol{\sigma}`, respectively.

The right-hand side :math:`\mathbf{s}` has values :math:`\mathbf{E_0}` on the boundary and 0 at inner edges. Values for :math:`\mathbf{E_0}` are obtained by solving a set of 1D problems for a given planewave polarization; either :math:`\mathbf{E_0} = E_x \, \hat{x}` or :math:`\mathbf{E_0} = E_y \, \hat{y}`. For explanation of the 1D solution, see Ward and Hohmann.

Once the electric field on cell edges has been computed, the electric (:math:`\mathbf{E}`) and magnetic (:math:`\mathbf{H}`) fields at observation locations can be obtain via the following:

.. math::
    \begin{align}
    \mathbf{E} &= \mathbf{Q_e \, u_e} = \mathbf{Q_c \, A_{e2c} \, u_e} \\
    \mathbf{H} &= \mathbf{Q_h \, u_e} = \frac{1}{i \omega} \mathbf{Q_c} \, diag(\boldsymbol{\mu}^{-1}) \, \mathbf{A_{f2c} C \, u_e}
    \end{align}

where :math:`\mathbf{Q_c}` represents the appropriate projection matrix from cell centers to a particular receiver (Ex, Ey, Hx, Hy or Hz).

To obtain impedance tensor (MT) or ZTEM data, we need the electric and/or magnetic fields for two orthogonal source polarizations; generally one in the x direction and one in the y direction. Let :math:`\mathbf{s}^{(1)}` and :math:`\mathbf{s}^{(2)}` denote the right-hand sides for source fields generated for each polarization. And let :math:`\mathbf{u_e}^{(1)}` and :math:`\mathbf{u_e}^{(2)}` denote the corresponding solutions for the electric fields on the edges. Then the electric fields (Ex or Ey) and magnetic fields (Hx, Hy or Hz) at some observation location can be expressed as:

.. math::
    \begin{align}
    E^{(j)} &= \mathbf{Q_e \, u_e}^{(j)} = \mathbf{Q_e \, A}(\sigma)^{-1} \, \mathbf{s}^{(j)} \;\;\; \textrm{for} \;\;\; j=1,2 \\
    H^{(j)} &= \mathbf{Q_h \, u_e}^{(j)} = \mathbf{Q_h \, A}(\sigma)^{-1} \, \mathbf{s}^{(j)} \;\;\; \textrm{for} \;\;\; j=1,2
    \end{align}
    :label: fields_at_loc

where the matrix

.. math::
    \mathbf{A}(\sigma) = \mathbf{C^T \, M_\mu \, C} + i\omega \mathbf{M_\sigma}

depends on the Earth's conductivity. If the fields at each observation location are known, MT data can be obtained using Eq. :eq:`impedance_tensor` and ZTEM data can be obtained using Eq. :eq:`transfer_fcn`.


.. Boundary Conditions
.. ^^^^^^^^^^^^^^^^^^^


.. Iterative Solver
.. ^^^^^^^^^^^^^^^^

.. For higher frequencies, the numerical solution to Eq. :eq:`discrete_e_sys` is fairly stable; as a large diagonal term results in a favourable conditioning number. However, MT and ZTEM sensors frequently measure low frequencies to image deeper targets. In this case, we must ensure the numerical solution to Eq. :eq:`discrete_e_sys` is stable. For this we use the following iterative solver approach.


Sensitivity
-----------

For use in the inversion, we require the sensitivity of the fields to the conductivities. Differentiating Eq. :eq:`discrete_e_sys` with respect to the conductivity model (:math:`\boldsymbol{\sigma}`), we obtain:

.. math::
    \frac{\partial \mathbf{A}}{\partial \boldsymbol{\sigma}} \mathbf{u_e} + \mathbf{A} \frac{\partial \mathbf{u_e}}{\partial \boldsymbol{\sigma}} = \mathbf{0}


where

.. math::
    \frac{\partial \mathbf{A}}{\partial \boldsymbol{\sigma}} = i \omega \, diag(\mathbf{u_e}) \, \mathbf{A_{e2c}^T V }


Thus the sensitivity of the fields to the conductivities is given by:

.. math::
    \frac{\partial \mathbf{u_e}}{\partial \boldsymbol{\sigma}} = - i\omega \mathbf{A}^{-1} diag(\mathbf{u_e}) \, \mathbf{A_{e2c}^T V }



.. _theory_inv:

Inverse Problem
---------------

To solve the inverse problem, we minimize the following global objective function:


.. math::
    \phi = \phi_d + \beta \phi_m
    :label:


where :math:`\phi_d` is the data misfit and :math:`\phi_m` is the model objective function. The data misfit 


where :math:`\Sigma` is a matrix of the inverse standard deviation for each measured data point :math:`\mathbf{d^{obs}}`. Due to the ill-posedness of the problem, there are no stable solutions and a regularization is needed. The regularization used penalizes for both smoothness, and likeness to a reference model :math:`\mathbf{m_{ref}}` supplied by the user.

.. math::
    \Phi_{reg} (\mathbf{m-m_{ref}}) = \frac{1}{2} \big \| \nabla (\mathbf{m - m_{ref}}) \big \|^2_2
    :label:

An important consideration comes when discretizing the regularization. The gradient operates on
cell centered variables in this instance. Applying a short distance approximation is second order
accurate on a domain with uniform cells, but only :math:`\mathcal{O}(1)` on areas where cells are non-uniform. To
rectify this a higher order approximation is used (:cite:`Haber2012`). The discrete regularization
operator can then be expressed as

.. math::
    \begin{align}
    \Phi_{reg}(\mathbf{m}) &= \frac{1}{2} \int_\Omega \big | \nabla m \big |^2 dV \\
    & \approx \frac{1}{2}  \beta \mathbf{ m^T G_c^T} \textrm{diag} (\mathbf{A_f^T v}) \mathbf{G_c m}
    \end{align}
    :label:

where :math:`\mathbf{A_f}` is an averaging matrix from faces to cell centres, :math:`\mathbf{G}` is the cell centre to cell face gradient operator, and v is the cell volume For the benefit of the user, let :math:`\mathbf{WTW}` be the weighting matrix given by

.. math::
    \mathbf{WTW} = \beta \mathbf{ G_c^T} \textrm{diag}(\mathbf{A_f^T v}) \mathbf{G_c m} =
    \begin{bmatrix} \mathbf{\alpha_x} & & \\ & \mathbf{\alpha_y} & \\ & & \mathbf{\alpha_z} \end{bmatrix} \big ( \mathbf{G_x^T \; G_y^T \; G_z^T} \big ) \textrm{diag} (\mathbf{v_f}) \begin{bmatrix} \mathbf{G_x} \\ \mathbf{G_y} \\ \mathbf{G_z} \end{bmatrix}
    :label:

where :math:`\alpha_i` for :math:`i=x,y,z` are diagonal matricies. In the code the WTW matrix is stored as a separate matrix so that individual model norm components can be calculated. Now, if a cell weighting is used it is applied to the entire norm, that is, there is a w for each cell.

.. math::
    \mathbf{WTW} = \textrm{diag} (w) \mathbf{WTW} \textrm{diag} (w)
    :label:

There is also the option of choosing a cell interface weighting. This allows for a weight on each cell FACE. The user must supply the weights (:math:`w_x, w_y, w_z` ) for each weighted cell. When the interface
weighting option is chosen and the value is less than 1, a sharp discontinuity will be created. When
the value is greater than 1, there will be a smooth transition. To prevent the inversion from putting
"junk" on the surface, the top X and Y face weights should have a large value.

.. math::
    \mathbf{WTW} = \mathbf{\alpha_x G_x^T} \textrm{diag} (w_x v_f) \mathbf{G_x} + \mathbf{\alpha_y G_y^T} \textrm{diag} (w_y v_f) \mathbf{G_y} + \mathbf{\alpha_z G_z^T} \textrm{diag} (w_z v_f) \mathbf{G_z}
    :label:

The resulting optimization problem is therefore:

.. math::
    \begin{align}
    &\min_m \;\; \Phi_{mis} (\mathbf{m}) + \beta \Phi_{reg}(\mathbf{m - m_{ref}}) \\
    &\; \textrm{s.t.} \;\; \mathbf{m_L \leq m \leq m_H}
    \end{align}
    :label:

where :math:`\beta` is a regularization parameter, and :math:`\mathbf{m_L}` and :math:`\mathbf{m_H}` are upper and lower bounds provided by some a prior geological information.
A simple Gauss-Newton optimization method is used where the system of equations is solved using ipcg (incomplete preconditioned conjugate gradients) to solve for each G-N step. For more
information refer again to :cite:`Haber2012` and references therein.



.. Data Misfit
.. -----------

.. MT data
.. ^^^^^^^

.. Here, we define a data misfit for MT data and express its derivative with respect to the model. From Eq. :eq:`impedance_tensor`, at a single observation location:

.. .. math::
..     \mathbf{ZH - E} = 
..     \begin{bmatrix} Z_{xx} H_x^{(1)} + Z_{xy} H_y^{(1)} - E_x^{(1)} \; & \; Z_{xx} H_x^{(2)} + Z_{xy} H_y^{(2)} - E_x^{(2)} \\
..     Z_{yx} H_x^{(1)} + Z_{yy} H_y^{(1)} - E_x^{(1)} \; & \; Z_{yx} H_x^{(2)} + Z_{yy} H_y^{(2)} - E_x^{(2)} \end{bmatrix} =
..     \begin{bmatrix} 0 & 0 \\ 0 & 0 \end{bmatrix}

.. For *N* observation stations, we can set up a sparse system:

.. .. math::
..     \mathbf{\tilde{Z}} \mathbf{\tilde{H}} - \mathbf{\tilde{E}} = \mathbf{0}
..     :label: Z_sys


.. Where :math:`\mathbf{Z_j}` is the impedance tensor for station *j*,

.. .. math::
..     \mathbf{\tilde{Z}} =
..     \begin{bmatrix} \mathbf{Z_1} & & & & & \\ & \ddots & & & & \\ & & \mathbf{Z_N} & & & \\ & & & \mathbf{Z_1} & & \\ & & & & \ddots & \\ & & & & & \mathbf{Z_N} \end{bmatrix} 

.. is a block diagonal matrix and the fields are stored in vectors:

.. .. math::
..     \mathbf{\tilde{H}} =
..     \begin{bmatrix} H_{x_1}^{(1)} \\ H_{y_1}^{(1)} \\ \vdots \\ H_{x_N}^{(1)} \\ H_{y_N}^{(1)} \\ H_{x_1}^{(2)} \\ H_{y_1}^{(2)} \\ \vdots \\ H_{x_N}^{(2)} \\ H_{y_N}^{(2)} \end{bmatrix}
..     \;\;\; \textrm{and} \;\;\;
..     \mathbf{\tilde{E}} =
..     \begin{bmatrix} E_{x_1}^{(1)} \\ E_{y_1}^{(1)} \\ \vdots \\ E_{x_N}^{(1)} \\ E_{y_N}^{(1)} \\ E_{x_1}^{(2)} \\ E_{y_1}^{(2)} \\ \vdots \\ E_{x_N}^{(2)} \\ E_{y_N}^{(2)} \end{bmatrix}


.. Using Eq. :eq:`fields_at_loc`, we can re-express Eq. :eq:`Z_sys` as:

.. .. math::
..     \mathbf{\tilde{Z}} \begin{bmatrix} \mathbf{\tilde{Q}_h u_e \!}^{(1)} \\ \mathbf{\tilde{Q}_h u_e \!}^{(2)} \end{bmatrix} - \begin{bmatrix} \mathbf{\tilde{Q}_e u_e \!}^{(1)} \\ \mathbf{\tilde{Q}_e u_e \!}^{(2)} \end{bmatrix}
..     = \Bigg ( \mathbf{\tilde{Z}} \begin{bmatrix} \mathbf{\tilde{Q}_h} & \\ & \mathbf{\tilde{Q}_h} \end{bmatrix} - \begin{bmatrix} \mathbf{\tilde{Q}_e} & \\ & \mathbf{\tilde{Q}_e} \end{bmatrix} \Bigg )
..     \begin{bmatrix} \mathbf{u_e \!}^{(1)} \\ \mathbf{u_e \!}^{(2)} \end{bmatrix}
..     = \mathbf{\tilde{Q}} \begin{bmatrix} \mathbf{u_e \!}^{(1)} \\ \mathbf{u_e \!}^{(2)} \end{bmatrix}
..     :label: mt_Q


.. Separating Eq. :eq:`mt_Q` into its real and imaginary components we obtain



.. ZTEM data
.. ^^^^^^^^^

.. From Eq. :eq:`transfer_fcn`, at a single observation location:



































.. OLD WAY DISCUSSED IN MANUAL I THINK WAS TRANSFERRED BLINDLY FROM MTZ3D. THE CODE ACUTALLY USES AN E-H FORMULATION

.. The solutions for the :math:`\mathbf{H}` and :math:`\mathbf{E}` fields are computed iteratively using the stabilized conjugate gradient method (BiCGstab). Because of the null space of the curl operator a discrete Helmholtz decomposition is used to write the electric field as

.. .. math::
..     \mathbf{E} = \mathbf{A} + \nabla \phi
..     :label:

.. where :math:`\mathbf{A}` is a vector potential and :math:`\phi` is a scalar potential. For MT or ZTEM data, :eq:`NSEM_system` is solved by eliminating the curl operator and solving for :math:`\mathbf{A}` and :math:`\phi`.

.. The forward problem of simulating data can now be written in the following form. Let :math:`\mathbf{D(m)}` be the discrete linear system obtained by the discretization of Maxwell's equations, where :math:`\mathbf{m} = log(\mathbf{\sigma})`.
.. The electric fields :math:`U` on the edges everywhere in the mesh are then:

.. .. math::
..     U(\sigma) = \mathbf{D(m)^{-1} S}
..     :label:

.. where :math:`\mathbf{S} = (s_1,s_2)` is the source for 2 polarizations and is approximated from a 1D MT solution and
.. interpolated to the entire mesh. The fields at the receivers locations are then

.. .. math::
..     \begin{align}
..     \mathbf{H} = Q_h u \\
..     \mathbf{E} = Q_e u
..     \end{align}

.. where

.. .. math::
..     Q_h = \dfrac{1}{i\omega\mu_0} Q_c A_{f2c} CURL
..     :label:

.. and

.. .. math::
..     Q_e = Q_c A_{e2c}
..     :label:

.. The matrix :math:`Q_c` is an interpolation matrix from cell centers to receiver locations, :math:`A_{f2c}` averages from faces to cell centers, and :math:`A_{e2c}` averages from edges to cell centers.






