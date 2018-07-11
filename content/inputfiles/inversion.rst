.. _e3dmt_input_inv:

Inversion Input File
====================

Version 1 (2014 and 2015)
-------------------------

Both **e3dMTinv.exe** and **e3dMTinv_iter.exe** use the same input file. The lines of input file are as follows:

.. tabularcolumns:: |L|C|C|

+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| Line # | Description                                                        | Description                                                       |
+========+====================================================================+===================================================================+
| 1      | :ref:`OcTree Mesh<e3dmt_input_inv_ln1>`                            | path to octree mesh file                                          |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 2      | :ref:`Observation File<e3dmt_input_inv_ln2>`                       | path to observations file                                         |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 3      | :ref:`1D Background Conductivity<e3dmt_input_inv_ln3>`             | 1D background conductivity model                                  |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 4      | :ref:`Initial Model<e3dmt_input_inv_ln4>`                          | initial model                                                     |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 5      | :ref:`Reference Model<e3dmt_input_inv_ln5>`                        | reference model                                                   |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 6      | :ref:`Background Susceptibility Model<e3dmt_input_inv_ln6>`        | background susceptibility model                                   |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 7      | :ref:`Active Topography Cells<e3dmt_input_inv_ln7>`                | topography                                                        |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 8      | :ref:`Active Model Cells<e3dmt_input_inv_ln8>`                     | active model cells                                                |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 9      | :ref:`Cell Weights<e3dmt_input_inv_ln9>`                           | additional cell weights                                           |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 10     | :ref:`Face Weights<e3dmt_input_inv_ln10>`                          | additional face weights                                           |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 11     | :ref:`beta_max beta_min beta_factor<e3dmt_input_inv_ln11>`         | cooling schedule for beta parameter                               |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 12     | :ref:`alpha_s alpha_x alpha_y alpha_z<e3dmt_input_inv_ln12>`       | weighting constants for smallness and smoothness constraints      |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 13     | :ref:`Chi Factor<e3dmt_input_inv_ln13>`                            | stopping criteria for inversion                                   |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 14     | :ref:`tol_nl mindm iter_per_beta<e3dmt_input_inv_ln14>`            | set the number of Gauss-Newton iteration for each beta value      |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 15     | :ref:`tol_ipcg max_iter_ipcg<e3dmt_input_inv_ln15>`                | set the tolerance and number of iterations for Gauss-Newton solve |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 16     | :ref:`Reference Model Update<e3dmt_input_inv_ln16>`                | reference model                                                   |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 17     | :ref:`Hard Constraints<e3dmt_input_inv_ln17>`                      | use *SMOOTH_MOD* or *SMOOTH_MOD_DIFF*                             |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 18     | :ref:`Bounds<e3dmt_input_inv_ln18>`                                | upper and lower bounds for recovered model                        |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+
| 19     | :ref:`BICG Parameters (Iterative .exe only)<e3dmt_input_inv_ln19>` | set solver parameters for iterative inversion                     |
+--------+--------------------------------------------------------------------+-------------------------------------------------------------------+



.. figure:: images/create_inv_input.png
     :align: center
     :width: 700

     Example input file for the inversion program (`Download <https://github.com/ubcgif/e3dmt/raw/master/assets/input_files1/e3dMT_octree_inv.inp>`__ ).


Line Descriptions
^^^^^^^^^^^^^^^^^

.. _e3dmt_input_inv_ln1:

    - **OcTree Mesh:** file path to the OcTree mesh file

.. _e3dmt_input_inv_ln2:

    - **Observation File:** file path to the :ref:`observed data file<obsFile>`

.. _e3dmt_input_inv_ln3:

    - **1D Background Conductivity:** The user may supply the file path to a `1D background conductivity model <http://em1dfm.readthedocs.io/en/latest/content/files/supporting.html#files-for-reference-and-starting-models>`__ , or if a homogeneous background conductivity is being used, the user may enter "VALUE" followed by a space and a numerical value (example "VALUE 0.01"). The way the 1D model is used to determine the boundary conditions for solving the full 3D problem depends on the active topography cells options on :ref:`line 7<e3dmt_input_inv_ln7>`. Before continuing, the user is urged to read the section on :ref:`boundary conditions <e3dmt_input_inv_bc>`.


.. important::

    - The number of layers in the 1D model for E3DMT must equal the number of underlying mesh cells in the vertical direction. Thus if underlying mesh for the OcTree mesh is 1028 by 1028 by 512, the 1D model must have 512 layer conductivities.
    - The boundary conditions computed using 1D models is only accurate when surface topography is minimal. In the case where surface topography is significant, it is suggested the user used E3DMT version 2.
 

.. _e3dmt_input_inv_ln4:

    - **Initial Model:** The user may supply the file path to an initial conductivity model. If a homogeneous conductivity value is being used for all active cells, the user can enter "VALUE" followed by a space and a numerical value; example "VALUE 0.01".

.. _e3dmt_input_inv_ln5:

    - **Reference Model:** The user may supply the file path to a reference conductivity model. If a homogeneous conductivity value is being used for all active cells, the user can enter "VALUE" followed by a space and a numerical value; example "VALUE 0.01".

.. _e3dmt_input_inv_ln6:

    - **Reference Susceptibility Model:** The user may supply the file path to a background susceptibility model. If the Earth is non-magnetic, the user may use the flag "NO_SUS".

.. _e3dmt_input_inv_ln7:

    - **Active Topography Cells:** Here, the user can choose to specify the cells which lie below the surface topography. To do this, the user may supply the file path to an active cells model file or type "ALL_ACTIVE". The active cells model has values 1 for cells lying below the surface topography and values 0 for cells lying above.

.. _e3dmt_input_inv_ln8:

    - **Active Model Cells:** Here, the user can choose to specify the model cells which are active during the inversion. To do this, the user may supply the file path to an active cells model file or type "ALL_ACTIVE". The active cells model has values 1 for cells lying below the surface topography and values 0 for cells lying above. Values for inactive cells are provided by the background conductivity model.

.. _e3dmt_input_inv_ln9:

    - **Cell Weights:** Here, the user specifies whether cell weights are supplied. If so, the user provides the file path to a :ref:`cell weights file <weightsFile>`  If no additional cell weights are supplied, the user enters "NO_WEIGHT".

.. _e3dmt_input_inv_ln10:

    - **Face Weights:** Here, the user specifies whether face weights are supplied. If so, the user provides the file path to a face weights file :ref:`cell weights file <weightsFile>`. If no additional cell weights are supplied, the user enters "NO_FACE_WEIGHT". The user may also enter "EKBLOM" for 1-norm approximation to recover sharper edges.

.. _e3dmt_input_inv_ln11:

    - **beta_max beta_min beta_factor:** Here, the user specifies protocols for the trade-off parameter (beta). *beta_max* is the initial value of beta, *beta_min* is the minimum allowable beta the program can use before quitting and *beta_factor* defines the factor by which beta is decreased at each iteration; example "1E4 10 0.2". The user may also enter "DEFAULT" if they wish to have beta calculated automatically.

.. _e3dmt_input_inv_ln12:

    - **alpha_s alpha_x alpha_y alpha_z:** `Alpha parameters <http://giftoolscookbook.readthedocs.io/en/latest/content/fundamentals/Alphas.html>`__ . Here, the user specifies the relative weighting between the smallness and smoothness component penalties on the recovered models.

.. _e3dmt_input_inv_ln13:

    - **Chi Factor:** The chi factor defines the target misfit for the inversion. A chi factor of 1 means the target misfit is equal to the total number of data observations.

.. _e3dmt_input_inv_ln14:

    - **tol_nl mindm iter_per_beta:** Here, the user specifies the number of Newton iterations. *tol_nl* is the Newton iteration tolerance (how close the gradient is to zero), *mindm* is the minimum model perturbation :math:`\delta m` allowed and iter_per_beta is the number of iterations per beta value.

.. _e3dmt_input_inv_ln15:

    - **tol_ipcg max_iter_ipcg:** Here, the user specifies solver parameters. *tol_ipcg* defines how well the iterative solver does when solving for :math:`\delta m` and *max_iter_ipcg* is the maximum iterations of incomplete-preconditioned-conjugate gradient.

.. _e3dmt_input_inv_ln16:

    - **Reference Model Update:** Here, the user specifies whether the reference model is updated at each inversion step result. If so, enter "CHANGE_MREF". If not, enter "NOT_CHANGE_MREF".

.. _e3dmt_input_inv_ln17:

    - **Hard Constraints:** SMOOTH_MOD runs the inversion without implementing a reference model (essential :math:`m_{ref}=0`). "SMOOTH_MOD_DIF" constrains the inversion in the smallness and smoothness terms using a reference model.

.. _e3dmt_input_inv_ln18:

    - **Bounds:** Bound constraints on the recovered model. Choose "BOUNDS_CONST" and enter the values of the minimum and maximum model conductivity; example "BOUNDS_CONST 1E-6 0.1". Enter "BOUNDS_NONE" if the inversion is unbounded, or if there is no a-prior information about the subsurface model.

.. _e3dmt_input_inv_ln19:

    - **BICG Parameters (omit line if using direct solver):** In order, the user specifies values for *tol_bicg*, *tol_ipcg_bicg*, *max_it_bicg* and *freq_Aphi*. For the practice example, the following was used: *1E-10 1E-5 100 -1*.

.. _e3dmt_input_inv_bc:

Details regarding boundary conditions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The way the 1D model is used to determine the boundary conditions for the full 3D problem depends on :ref:`background conductivity (line 3)<e3dmt_input_inv_ln3>` and the :ref:`active topography cells (line 7) <e3dmt_input_inv_ln7>`. This can be explained as follows:

        - Assume *VALUE* is used to define the 1D background model (line 3) and the flag *ALL_ACTIVE* is used to define active topography cells (line 7). Then the boundary conditions are obtained by solving the fields for a whole space. This approach is strongly discouraged!

        - Assume *VALUE* is used to define the 1D background model (line 3) and an *active cells model* is used to define the active topography cells (line 7). Then the highest surface elevation in the active cells model is used as the surface elevation for the 1D model. Below this surface, the background conductivity is equal to the specified value. Above this surface, the background conductivity is set to air.

        - Assume a *1D model* defines the background conductivity (line 3) and the flag *ALL_ACTIVE* is used to define active topography cells (line 7). The top of the 1D model corresponds to the top of the OcTree mesh when solving the 1D problem. As a result, it is important to include air cells in the 1D model.

        - Assume a *1D model* defines the background conductivity (line 3) and an *active cells model* is used to define the active topography cells (line 7). Then the highest surface elevation in the active cells model is used as the surface elevation for the 1D model. The 1D problem is still solved and the top of the 1D model still corresponds to the top of the OcTree mesh. However, all layers above the surface are set to air regardless of the values specified in the 1D model.



.. _e3dmt_input_inv2:

Version 2 (2017)
----------------

Both the forward and inverse problems are solved using the **e3dMTinv_ver2** executable program. In both cases, the lines of the input file are the same. However in the case of forward modeling, some lines in the input file are not used by the code and can be given any value. The lines of input file are as follows:

.. tabularcolumns:: |L|C|C|

+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| Line # | Parameter                                                    | Description                                                             |
+========+==============================================================+=========================================================================+
| 1      |:ref:`OcTree Mesh<e3dmt_input_inv2_ln1>`                      | path to octree mesh file                                                |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 2      |:ref:`Observation File<e3dmt_input_inv2_ln2a>`                | path to observations file                                               |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 3      |:ref:`Receiver File<e3dmt_input_inv2_ln2b>`                   | path to receivers file                                                  |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 4      |:ref:`Frequencies File<e3dmt_input_inv2_ln2c>`                | path to frequencies file                                                |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 5      |:ref:`Background Conductivity<e3dmt_input_inv2_ln3>`          | set background conductivity                                             |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 6      |:ref:`Initial/FWD Model<e3dmt_input_inv2_ln4>`                | initial model                                                           |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 7      |:ref:`Reference Model<e3dmt_input_inv2_ln5>`                  | reference model                                                         |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 8      |:ref:`Background Susceptibility Model<e3dmt_input_inv2_ln6>`  | background susceptibility                                               |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 9      |:ref:`Active Topography Cells<e3dmt_input_inv2_ln7>`          | topography                                                              |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 10     |:ref:`Active Model Cells<e3dmt_input_inv2_ln8>`               | active model cells                                                      |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 11     |:ref:`Cell Weights<e3dmt_input_inv2_ln9>`                     | additional cell weights                                                 |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 12     |:ref:`Face Weights<e3dmt_input_inv2_ln10>`                    | additional face weights                                                 |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 13     |:ref:`Norm Sparseness<e3dmt_input_inv2_ln11>`                 | set parameters to recover smooth, sparse or blocky models               |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 14     |:ref:`beta_max beta_min beta_factor<e3dmt_input_inv2_ln12>`   | cooling schedule for beta parameter                                     |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 15     |:ref:`alpha_s alpha_x alpha_y alpha_z<e3dmt_input_inv2_ln13>` | weighting constants for smallness and smoothness constraints            |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 16     |:ref:`Chi Factor<e3dmt_input_inv2_ln14>`                      | stopping criteria for inversion                                         |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 17     |:ref:`iter_per_beta nBetas<e3dmt_input_inv2_ln15>`            | set the number of Gauss-Newton iteration for each beta value            |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 18     |:ref:`tol_ipcg max_iter_ipcg<e3dmt_input_inv2_ln16>`          | set the tolerance and number of iterations for Gauss-Newton solve       |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 19     |:ref:`Reference Model Update<e3dmt_input_inv2_ln17>`          | reference model                                                         |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 20     |:ref:`Hard Constraints<e3dmt_input_inv2_ln18>`                | use *SMOOTH_MOD* or *SMOOTH_MOD_DIFF*                                   |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 21     |:ref:`Bounds<e3dmt_input_inv2_ln19>`                          | upper and lower bounds for recovered model                              |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 22     |:ref:`Memory Options<e3dmt_input_inv2_ln20>`                  | options for storing factorizations of forward system (RAM vs disk)      |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 23     |:ref:`Phase Convention<e3dmt_input_inv2_ln21>`                | set data convention to :math:`e^{-i\omega t}` or :math:`e^{+i\omega t}` |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+



.. .. figure:: images/e3dmt_inv_input2.png
..      :align: center
..      :width: 700

..      Example input file for the inversion program.


Line Descriptions
^^^^^^^^^^^^^^^^^

.. _e3dmt_input_inv2_ln1:

    - **OcTree Mesh:** file path to the :ref:`octree mesh file<octreeFile>`

.. _e3dmt_input_inv2_ln2a:

    - **Observation File:** file path to the :ref:`observed data file<obsFile2>`

.. _e3dmt_input_inv2_ln2b:

    - **Receiver File:** file path to the :ref:`receiver file<receiverFile>`

.. _e3dmt_input_inv2_ln2c:

    - **Frequencies File:** file path to the :ref:`frequencies file<freqFile>`

.. _e3dmt_input_inv2_ln3:

    - **Background Conductivity:** On this line, the user first specifies a flag for the background conductivity model ('1DBACKGROUND' or '3DBACKGROUND'). Next, the user may supply the file path to the corresponding conductivity model (ex: *1DBACKGROUND model1d.con*), or if a homogeneous background conductivity is being used, the user may enter "VALUE" followed by a space and a numerical value (ex: *3DBACKGROUND VALUE 0.01*). The way the background model is used to determine the boundary conditions for solving NSEM problem depends on the active topography cells options on :ref:`line 9<e3dmt_input_inv2_ln7>`. Before continuing, the user is urged to read the section on :ref:`boundary conditions <e3dmt_input_inv2_bc>`.


.. important::

    - The number of layers in the 1D model for E3DMT ver 2 must equal the number of underlying mesh cells in the vertical direction. Thus if underlying mesh for the OcTree mesh is 1028 by 1028 by 512, the 1D model must have 512 layer conductivities.
    - The boundary conditions computed using 1D models is only accurate when surface topography is minimal. In the case where surface topography is significant, 3D background models are suggested.


.. _e3dmt_input_inv2_ln4:

    - **Initial/FWD Model:** On this line we specify either the starting model for the inversion or the conductivity model for the forward modeling. On this line, there are 3 possible options:

        - If the program is being used to forward model data, the flag 'FWDMODEL' is entered followed by the path to the conductivity model.
        - If the program is being used to invert data, only the path to a conductivity model is required; e.g. inversion is assumed unless otherwise specified.
        - If a homogeneous conductivity value is being used as the starting model for an inversion, the user can enter "VALUE" followed by a space and a numerical value; example "VALUE 0.01".


.. important::

    If data are only being forward modeled, only the :ref:`background susceptibility model<e3dmt_input_inv2_ln6>`, :ref:`active topography cells<e3dmt_input_inv2_ln7>` and :ref:`tol_ipcg max_iter_ipcg<e3dmt_input_inv2_ln16>` fields are relevant. **However**, the remaining fields must not be empty and must have correct syntax for the code to run.


.. _e3dmt_input_inv2_ln5:

    - **Reference Model:** The user may supply the file path to a reference conductivity model. If a homogeneous conductivity value is being used for all active cells, the user can enter "VALUE" followed by a space and a numerical value; example "VALUE 0.01".

.. _e3dmt_input_inv2_ln6:

    - **Background Susceptibility Model:** The user may supply the file path to a background susceptibility model. If the Earth is non-magnetic, the user may use the flag "NO_SUS".

.. _e3dmt_input_inv2_ln7:

    - **Active Topography Cells:** Here, the user can choose to specify the cells which lie below the surface topography. To do this, the user may supply the file path to an active cells model file or type "ALL_ACTIVE". The active cells model has values 1 for cells lying below the surface topography and values 0 for cells lying above.

.. _e3dmt_input_inv2_ln8:

    - **Active Model Cells:** Here, the user can choose to specify the model cells which are active during the inversion. To do this, the user may supply the file path to an active cells model file or type "ALL_ACTIVE". The active cells model has values 1 for cells lying below the surface topography and values 0 for cells lying above. Values for inactive cells are provided by the background conductivity model.

.. _e3dmt_input_inv2_ln9:

    - **Cell Weights:** Here, the user specifies whether cell weights are supplied. If so, the user provides the file path to a :ref:`cell weights file <weightsFile>`  If no additional cell weights are supplied, the user enters "NO_WEIGHT".

.. _e3dmt_input_inv2_ln10:

    - **Face Weights:** Here, the user specifies whether face weights are supplied. If so, the user provides the file path to a face weights file :ref:`cell weights file <weightsFile>`. If no additional cell weights are supplied, the user enters "NO_FACE_WEIGHT". The user may also enter "EKBLOM" for 1-norm approximation to recover sharper edges.

.. _e3dmt_input_inv2_ln11:

    - **Sparseness:** The sparseness of the recovered model is determined by the terms within the `model objective function <http://giftoolscookbook.readthedocs.io/en/latest/content/fundamentals/Norms.html>`__ . A standard approach is to use an L2-norm for all terms

        - To use the L2-norm, enter the flag 'USE_L2'
        - To specify the Ekblom norm, enter the flag 'USE_EKBLOM' followed by values for :math:`p` and :math:`\varepsilon` where the Ekblom norm is given by:


.. math::
    \sum_{i=1}^M \, (\sigma_i^2 + \varepsilon^2)^{p/2} \;\;\; \textrm{s.t.} \;\;\; 1\leq p \leq 2, \; \varepsilon > 0



.. _e3dmt_input_inv2_ln12:

    - **beta_max beta_min beta_factor:** Here, the user specifies protocols for the trade-off parameter (beta). *beta_max* is the initial value of beta, *beta_min* is the minimum allowable beta the program can use before quitting and *beta_factor* defines the factor by which beta is decreased at each iteration; example "1E4 10 0.2". The user may also enter "DEFAULT" if they wish to have beta calculated automatically.

.. _e3dmt_input_inv2_ln13:

    - **alpha_s alpha_x alpha_y alpha_z:** `Alpha parameters <http://giftoolscookbook.readthedocs.io/en/latest/content/fundamentals/Alphas.html>`__ . Here, the user specifies the relative weighting between the smallness and smoothness component penalties on the recovered models.

.. _e3dmt_input_inv2_ln14:

    - **Chi Factor:** The chi factor defines the target misfit for the inversion. A chi factor of 1 means the target misfit is equal to the total number of data observations.

.. _e3dmt_input_inv2_ln15:

    - **iter_per_beta nBetas:** Here, *iter_per_beta* is the number of iterations per beta value. **define nBetas**

.. _e3dmt_input_inv2_ln16:

    - **tol_ipcg max_iter_ipcg:** Here, the user specifies solver parameters. *tol_ipcg* defines how well the iterative solver does when solving for :math:`\delta m` and *max_iter_ipcg* is the maximum iterations of incomplete-preconditioned-conjugate gradient.

.. _e3dmt_input_inv2_ln17:

    - **Reference Model Update:** Here, the user specifies whether the reference model is updated at each inversion step result. If so, enter "CHANGE_MREF". If not, enter "NOT_CHANGE_MREF".

.. _e3dmt_input_inv2_ln18:

    - **Hard Constraints:** SMOOTH_MOD runs the inversion without implementing a reference model (essential :math:`m_{ref}=0`). "SMOOTH_MOD_DIF" constrains the inversion in the smallness and smoothness terms using a reference model.

.. _e3dmt_input_inv2_ln19:

    - **Bounds:** Bound constraints on the recovered model. Choose "BOUNDS_CONST" and enter the values of the minimum and maximum model conductivity; example "BOUNDS_CONST 1E-6 0.1". Enter "BOUNDS_NONE" if the inversion is unbounded, or if there is no a-prior information about the subsurface model.

.. _e3dmt_input_inv2_ln20:

    - **Memory Options:** This code uses a factorization to solve the forward system at each frequency. These factorizations must be stored. By using the flag 'FACTOR_IC' (in cpu), factorizations are stored within a computer's RAM. Although this is faster, larger problems cannot be solved if insufficient temporary memory is available. The factorizations are stored in permanent memory (disk) if the flag 'FACTOR_OOC' (out of cpu) is used followed by the path to a directory. This is slower because the program must read these files many times. The second options is ill-advised if files are being transferred over a network.


.. _e3dmt_input_inv2_ln21:

    - **Phase Convention:** If the predicted/observed data have a sign convention :math:`e^{+i \omega t}` use the flag 'PLUS_IOMEGA'. If the predicted/observed data have a sign convention :math:`e^{-i \omega t}` use the flag 'MINUS_IOMEGA'.



.. _e3dmt_input_inv2_bc:

Details regarding boundary conditions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The way background models are used to determine the boundary conditions for the problem depends on :ref:`background conductivity (line 5)<e3dmt_input_inv2_ln3>` and the :ref:`active topography cells (line 9) <e3dmt_input_inv_ln7>`. This can be explained as follows:

**1DBACKGROUND:**

        - Assume *VALUE* is used to define the 1D background model (line 5) and the flag *ALL_ACTIVE* is used to define active topography cells (line 9). Then the boundary conditions are obtained by solving the fields for a whole space. This approach is strongly discouraged!

        - Assume *VALUE* is used to define the 1D background model (line 5) and an *active cells model* is used to define the active topography cells (line 9). Then the highest surface elevation in the active cells model is used as the surface elevation for the 1D model. Below this surface, the background conductivity is equal to the specified value. Above this surface, the background conductivity is set to air.

        - Assume a *1D model* defines the background conductivity (line 5) and the flag *ALL_ACTIVE* is used to define active topography cells (line 9). The top of the 1D model corresponds to the top of the OcTree mesh when solving the 1D problem. As a result, it is important to include air cells in the 1D model.

        - Assume a *1D model* defines the background conductivity (line 5) and an *active cells model* is used to define the active topography cells (line 9). Then the highest surface elevation in the active cells model is used as the surface elevation for the 1D model. The 1D problem is still solved and the top of the 1D model still corresponds to the top of the OcTree mesh. However, all layers above the surface are set to air regardless of the values specified in the 1D model.


**3DBACKGROUND:**

        - Assume *VALUE* is used to define the 3D background model (line 5) and the flag *ALL_ACTIVE* is used to define active topography cells (line 9). Then the boundary conditions are obtained by solving the fields for a whole space. This approach is strongly discouraged!

        - Assume *VALUE* is used to define the 3D background model (line 5) and an *active cells model* is used to define the active topography cells (line 9). A 3D problem is solved where all cells below the surface are set to the specified value and all the cells above the surface are set to air.

        - Assume a *3D model* defines the background conductivity (line 5) and the flag *ALL_ACTIVE* is used to define active topography cells (line 9). A 3D problem is solved for the specified background model.

        - Assume a *1D model* defines the background conductivity (line 5) and an *active cells model* is used to define the active topography cells (line 9). A 3D problem is solved where all cells above the surface are set to air, regardless of the values specified in the model.
