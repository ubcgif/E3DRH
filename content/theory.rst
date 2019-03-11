.. _theory:

Background Theory
=================

This section aims to provide the user with a basic review of the physics, discretization, and optimization
techniques used to solve the frequency domain electromagnetics problem. It is assumed
that the user has some background in these areas. For further reading see (:cite:`Nabighian1991`).

.. important::

    This code uses the following coordinate system and Fourier convention to solve Maxwell's equations:
        - X = Easting, Y = Northing, Z +ve downward (left-handed)
        - An :math:`e^{-i \omega t}` Fourier convention

.. _theory_fundamentals:

Fundamental Physics
-------------------

Maxwell's equations provide the starting point from which an understanding of how electromagnetic
fields can be used to uncover the substructure of the Earth. In the frequency domain Maxwell's
equations are:

.. math::
    \begin{align}
        \nabla \times &\mathbf{E} - i\omega\mu \mathbf{H} = 0 \\
        \nabla \times &\mathbf{H} - \sigma \mathbf{E} = \mathbf{s} \\
        &\mathbf{\hat{n} \times H} = 0
    \end{align}
    :label: maxwells_eq

where :math:`\mathbf{E}` and :math:`\mathbf{H}` are the electric and magnetic fields, :math:`\mathbf{s}` is some external source and :math:`e^{-i\omega t}` is suppressed.
Symbols :math:`\mu`, :math:`\sigma` and :math:`\omega` are the magnetic permeability, conductivity, and angular frequency, respectively. This formulation assumes a quasi-static mode so that the system can be viewed as a diffusion equation (Weaver, 1994; Ward and Hohmann, 1988 in :cite:`Nabighian1991`). By doing so, some difficulties arise when
solving the system;

    - the curl operator has a non-trivial null space making the resulting linear system highly ill-conditioned
    - the conductivity :math:`\sigma` varies over several orders of magnitude
    - the fields can vary significantly near the sources, but smooth out at distance thus high resolution is required near sources


Octree Mesh
-----------

By using an Octree discretization of the earth domain, the areas near sources and likely model
location can be give a higher resolution while cells grow large at distance. In this manner, the
necessary refinement can be obtained without added computational expense. The figure below shows an
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

To solve the forward problem, we must first discretize and solve for the fields in Eq. :eq:`maxwells_eq`, where :math:`e^{-i\omega t}` is suppressed. Using finite volume discretization, the electric fields on cell edges (:math:`\mathbf{u_e}`) are obtained by solving the following system at every frequency:

.. math::
    \big [ \mathbf{C^T \, M_\mu \, C} + i\omega \mathbf{M_\sigma} \big ] \, \mathbf{u_e} = - i \omega \mathbf{s}
    :label: discrete_e_sys

where :math:`\mathbf{C}` is the curl operator and:

.. math::
    \begin{align}
    \mathbf{M_\mu} &= diag \big ( \mathbf{A^T_{f2c} V} \, \boldsymbol{\mu^{-1}} \big ) \\
    \mathbf{M_\sigma} &= diag \big ( \mathbf{A^T_{e2c} V} \, \boldsymbol{\sigma} \big ) \\
    \end{align}

where :math:`\mathbf{V}` is a diagonal matrix containing  all cell volumes, :math:`\mathbf{A_{f2c}}` averages from faces to cell centres and :math:`\mathbf{A_{e2c}}` averages from edges to cell centres. The magnetic permeabilities and conductivities for each cell are contained within vectors :math:`\boldsymbol{\mu}` and :math:`\boldsymbol{\sigma}`, respectively.

E3D version 2 data represent the component of the total magnetic field that is parallel to the dipole moment of the loop receiver. To compute this, we approximate the integral formulation of Faraday's law as:

.. math::
    \sum_{i=1}^N \, \big (\mathbf{P_i \, u_e})^T \, \boldsymbol{\ell_i} = i \omega \mu \mathbf{H_i}^T \mathbf{a}
    :label: faraday_law

where :math:`i` denotes a particular loop segment, :math:`\mathbf{P_i}` is a projection matrix from cell edges to a particular segment and :math:`\boldsymbol{\ell_i}` is the vector distance for a particular segment. :math:`\mathbf{H_i}` is the total magnetic field at the center of the loop and :math:`\mathbf{a}` is the vector cross-sectional area of the loop. If we let :math:`\bar{H_i}` be the dot product of :math:`\mathbf{H_i}` and the unit vector direction of :math:`\mathbf{a}`, then

.. math::
    \bar{H_i} = \frac{1}{i\omega} \, \mathbf{Q_i \, u_e}


where :math:`\mathbf{Q_i}` is a just a linear operator that integrates the electric field over the path of the receiver loop and normalizes by :math:`\mu` and the cross-sectional area. The projection matrix for all receivers can be amalgamated to form a single linear operator (:math:`\mathbf{Q}`) such that the data is given by:

.. math::
    \mathbf{d} = \frac{1}{i\omega} \mathbf{Q \, u_e} = - \mathbf{Q \, A}(\sigma)^{-1} \mathbf{s}
    :label: fwd_solution


where

.. math::
    \mathbf{A}(\sigma) = \mathbf{C^T \, M_\mu \, C} + i\omega \mathbf{M_\sigma}
    :label: A_operator


Sensitivity
-----------

The data are split into their real and imaginary components. Thus the data at a particular frequency for a particular reading is organized in a vector of the form:

.. math::
    \mathbf{d} = [\mathbf{d}^\prime, \mathbf{d}^{\prime \prime}]^T
    :label: data_vector


where :math:`\prime` denotes real components and :math:`\prime\prime` denotes imaginary components. To determine the sensitivity of the data (i.e. :eq:`data_vector`) with respect to the model (:math:`\boldsymbol{\sigma}`), we must compute:

.. math::
    \frac{\partial \mathbf{d}}{\partial \boldsymbol{\sigma}} = \Bigg [ 
    \dfrac{\partial \mathbf{d}^\prime}{\partial \boldsymbol{\sigma}} ,
    \dfrac{\partial \mathbf{d}^{\prime\prime}}{\partial \boldsymbol{\sigma}} \Bigg ]^T


where the conductivity model :math:`\boldsymbol{\sigma}` is real-valued. To differentiate the data with with respect to the model, we require the derivative of the electric fields on cell edges (:math:`\mathbf{u_e}`) with respect to the model (Eq. :eq:`fwd_solution`). This is given by:

.. math::
    \frac{\partial \mathbf{u_e}}{\partial \boldsymbol{\sigma}} = - i\omega \mathbf{A}^{-1} diag(\mathbf{u_e}) \, \mathbf{A_{e2c}^T V }
    :label: sensitivity_fields









.. _theory_inv:


Inverse Problem
---------------

To solve the inverse problem, we minimize the following global objective function:


.. math::
    \phi = \phi_d + \beta \phi_m
    :label: global_objective


where :math:`\phi_d` is the data misfit and :math:`\phi_m` is the model objective function. The data misfit ensures the recovered model adequately explains the set of field observations. The model objective function adds geological constraints to the recovered model.

Data Misfit
^^^^^^^^^^^

The data misfit is represented as the L2-norm of a weighted residual between the observed data (:math:`d_{obs}`) and the predicted data for a given conductivity model :math:`\boldsymbol{\sigma}`, i.e.:

.. math::
    \phi_d = \big \| \mathbf{W_d} \big ( \mathbf{d_{obs}} - \mathbb{F}[\boldsymbol{\sigma}] \big ) \big \|^2
    :label: data_misfit_2


where :math:`W_d` is a diagonal matrix containing the reciprocals of the uncertainties :math:`\boldsymbol{\varepsilon}` for each measured data point, i.e.:

.. math::
    \mathbf{W_d} = \textrm{diag} \big [ \boldsymbol{\varepsilon}^{-1} \big ] 


.. important:: For a better understanding of the data misfit, see the `GIFtools cookbook <http://giftoolscookbook.readthedocs.io/en/latest/content/fundamentals/Uncertainties.html>`__ .


Model Objective Function
^^^^^^^^^^^^^^^^^^^^^^^^

Due to the ill-posedness of the problem, there are no stable solutions obtain by freely minimizing the data misfit, and thus regularization is needed. The regularization used penalties for both smoothness, and likeness to a reference model :math:`\mathbf{m_{ref}}` supplied by the user.

.. math::
    \phi_m (\mathbf{m-m_{ref}}) = \frac{1}{2} \big \| \nabla (\mathbf{m - m_{ref}}) \big \|^2_2
    :label:

An important consideration comes when discretizing the regularization. The gradient operates on
cell centered variables in this instance. Applying a short distance approximation is second order
accurate on a domain with uniform cells, but only :math:`\mathcal{O}(1)` on areas where cells are non-uniform. To
rectify this a higher order approximation is used (:cite:`Haber2012`). The discrete regularization
operator can then be expressed as

.. math::
    \begin{align}
    \phi_m(\mathbf{m}) &= \frac{1}{2} \int_\Omega \big | \nabla m \big |^2 dV \\
    & \approx \frac{1}{2}  \beta \mathbf{ m^T G_c^T} \textrm{diag} (\mathbf{A_f^T v}) \mathbf{G_c m}
    \end{align}
    :label:

where :math:`\mathbf{A_f}` is an averaging matrix from faces to cell centres, :math:`\mathbf{G}` is the cell centre to cell face gradient operator, and v is the cell volume For the benefit of the user, let :math:`\mathbf{R^T R}` be the weighting matrix given by:

.. math::
    \mathbf{R^T R} = \beta \mathbf{ G_c^T} \textrm{diag}(\mathbf{A_f^T v}) \mathbf{G_c m} =
    \begin{bmatrix} \mathbf{\alpha_x} & & \\ & \mathbf{\alpha_y} & \\ & & \mathbf{\alpha_z} \end{bmatrix} \big ( \mathbf{G_x^T \; G_y^T \; G_z^T} \big ) \textrm{diag} (\mathbf{v_f}) \begin{bmatrix} \mathbf{G_x} \\ \mathbf{G_y} \\ \mathbf{G_z} \end{bmatrix}
    :label:

where :math:`\alpha_i` for :math:`i=x,y,z` are diagonal matricies. In the code the :math:`\mathbf{R^T R}` matrix is stored as a separate matrix so that individual model norm components can be calculated. Now, if a cell weighting is used it is applied to the entire norm, that is, there is a w for each cell.

.. math::
    \mathbf{R^T R} = \textrm{diag} (w) \mathbf{W^T W} \textrm{diag} (w)
    :label:

There is also the option of choosing a cell interface weighting. This allows for a weight on each cell FACE. The user must supply the weights (:math:`w_x, w_y, w_z` ) for each weighted cell. When the interface weighting option is chosen and the value is less than 1, a sharp discontinuity will be created. When
the value is greater than 1, there will be a smooth transition. To prevent the inversion from putting
"junk" on the surface, the top X and Y face weights should have a large value.

.. math::
    \mathbf{R^T R} = \mathbf{\alpha_x G_x^T} \textrm{diag} (w_x v_f) \mathbf{G_x} + \mathbf{\alpha_y G_y^T} \textrm{diag} (w_y v_f) \mathbf{G_y} + \mathbf{\alpha_z G_z^T} \textrm{diag} (w_z v_f) \mathbf{G_z}
    :label: MOF

The resulting optimization problem is therefore:

.. math::
    \begin{align}
    &\min_m \;\; \phi_d (\mathbf{m}) + \beta \phi_m(\mathbf{m - m_{ref}}) \\
    &\; \textrm{s.t.} \;\; \mathbf{m_L \leq m \leq m_H}
    \end{align}
    :label: inverse_problem

where :math:`\beta` is a regularization parameter, and :math:`\mathbf{m_L}` and :math:`\mathbf{m_H}` are upper and lower bounds provided by some a prior geological information.
A simple Gauss-Newton optimization method is used where the system of equations is solved using ipcg (incomplete preconditioned conjugate gradients) to solve for each G-N step. For more
information refer again to :cite:`Haber2012` and references therein.


.. _theory_sparse:

Sparse Norms
^^^^^^^^^^^^

The Ekblom regularization allows the user to essentially change the norm or distance measure of the regularization. The discrete Ekblom norm is given by

.. math::
    \phi_E = \mathbf{V^T} \big [ \mathbf{A_f} \big [ \mathbf{G} [\mathbf{m - m_{ref}} ] \big ]^2 + \epsilon \big ]^p


where

    - :math:`\mathbf{G}` is the gradient operator
    - :math:`\epsilon` is a threshold value 
    - :math:`p` specifies the norm 
    
The threshold value (:math:`\epsilon`) acts as a means of stability for the Ekblom norm and is usually chosen to be several orders of magnitude lower than the smallest reasonable model value (:math:`\sim 10^{-8}`). The parameter :math:`p` is best chosen to be between 1 and 2; where :math:`p` = 1 recovers more compact models and :math:`p` = 2 recovers smoother models. When incorporated into the regularization, the model objective function becomes:

.. math::
    \mathbf{R^T R} = \mathbf{G^T} \textrm{diag} \Big ( \mathbf{A_f^T v} \big [ \mathbf{A_f} [\mathbf{G} (\mathbf{m - m_{ref}}) ] \big ]^2 + \epsilon \big ]^{p-1} \Big ) \mathbf{G}



Inversion Parameters and Tolerances
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _theory_cooling:

Cooling Schedule
~~~~~~~~~~~~~~~~

Our goal is to solve Eq. :eq:`inverse_problem`, i.e.:

.. math::
    \begin{align}
    &\min_m \;\; \phi_d (\mathbf{m}) + \beta \phi_m(\mathbf{m - m_{ref}}) \\
    &\; \textrm{s.t.} \;\; \mathbf{m_L \leq m \leq m_H}
    \end{align}

but how do we choose an acceptable trade-off parameter :math:`\beta`? For this, we use a cooling schedule. This is described in the `GIFtools cookbook <http://giftoolscookbook.readthedocs.io/en/latest/content/fundamentals/Beta.html>`__ . The cooling schedule can be defined using the following parameters:

    - **beta_max:** The initial value for :math:`\beta`
    - **beta_factor:** The factor at which :math:`\beta` is decrease to a subsequent solution of Eq. :eq:`inverse_problem`
    - **beta_min:** The minimum :math:`\beta` for which Eq. :eq:`inverse_problem` is solved before the inversion will quit (E3D version 1 only)
    - **nBetas:** The number of times the inversion code will decrease :math:`\beta` and solve Eq. :eq:`inverse_problem` before it quits (E3D version 2 only)
    - **Chi Factor:** The inversion program stops when the data misfit :math:`\phi_d = N \times Chi \; Factor`, where :math:`N` is the number of data observations

.. _theory_GN:

Gauss-Newton Update
~~~~~~~~~~~~~~~~~~~

For a given trade-off parameter (:math:`\beta`), the model :math:`\mathbf{m}` is updated using the Gauss-Newton approach. Because the problem is non-linear, several model updates may need to be completed for each :math:`\beta`. Where :math:`k` denotes the Gauss-Newton iteration, we solve:

.. math::
    \mathbf{H}_k \, \mathbf{\delta m}_k = - \nabla \phi_k
    :label: GN_gen


using the current model :math:`\mathbf{m}_k` and update the model according to:

.. math::
    \mathbf{m}_{k+1} = \mathbf{m}_{k} + \alpha \mathbf{\delta m}_k
    :label: GN_update


where :math:`\mathbf{\delta m}_k` is the step direction, :math:`\nabla \phi_k` is the gradient of the global objective function, :math:`\mathbf{H}_k` is an approximation of the Hessian and :math:`\alpha` is a scaling constant. This process is repeated until any of the following occurs:

    1. The gradient is sufficiently small, i.e.:

        .. math::
            \| \nabla \phi_k \|^2 < \textrm{tol_nl}

    2. The smallest component of the model perturbation its small in absolute value, i.e.:

        .. math::
            \textrm{max} ( |\mathbf{\delta m}_k | ) < mindm

    3. A max number of GN iterations have been performed, i.e.

        .. math::
            k = \textrm{iter_per_beta} 


.. _theory_IPCG:

Gauss-Newton Solve
~~~~~~~~~~~~~~~~~~

Here we discuss the details of solving Eq. :eq:`GN_gen` for a particular Gauss-Newton iteration :math:`k`. Using the data misfit from Eq. :eq:`data_misfit_2` and the model objective function from Eq. :eq:`MOF`, we must solve:

.. math::
    \Big [ \mathbf{J^T W_d^T W_d J + \beta \mathbf{W^T W}} \Big ] \mathbf{\delta m}_k =
    - \Big [ \mathbf{J^T W_d^T W_d } \big ( \mathbf{d_{obs}} - \mathbb{F}[\mathbf{m}_k] \big ) + \beta \mathbf{W^T W m}_k \Big ]
    :label: GN_expanded


where :math:`\mathbf{J}` is the sensitivity of the data to the current model :math:`\mathbf{m}_k`. The system is solved for :math:`\mathbf{\delta m}_k` using the incomplete-preconditioned-conjugate gradient (IPCG) method. This method is iterative and exits with an approximation for :math:`\mathbf{\delta m}_k`. Let :math:`i` denote an IPCG iteration and let :math:`\mathbf{\delta m}_k^{(i)}` be the solution to :eq:`GN_expanded` at the :math:`i^{th}` IPCG iteration, then the algorithm quits when:

    1. the system is solved to within some tolerance and additional iterations do not result in significant increases in solution accuracy, i.e.:

        .. math::
            \| \mathbf{\delta m}_k^{(i-1)} - \mathbf{\delta m}_k^{(i)} \|^2 / \| \mathbf{\delta m}_k^{(i-1)} \|^2 < \textrm{tol_ipcg}


    2. a maximum allowable number of IPCG iterations has been completed, i.e.:

        .. math::
            i = \textrm{max_iter_ipcg}


