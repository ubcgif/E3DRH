.. _aem_input_inv:

Inversion Input File
====================

Both the forward and inverse problems are solved using the **AEM.exe** executable program. In both cases, the lines of the input file are the same. However in the case of forward modeling, some lines in the input file are not used by the code and can be given any value. The lines of input file are as follows:

.. tabularcolumns:: |L|C|C|

+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| Line # | Parameter                                                    | Description                                                             |
+========+==============================================================+=========================================================================+
| 1      |:ref:`Inversion Mesh<aem_input_inv2_ln1>`                     | path to inversion mesh file                                             |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 2      |:ref:`Forward Mesh<aem_input_inv2_ln2>`                       | path to forward mesh file                                               |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 3      |:ref:`Observations File<aem_input_inv2_ln3>`                  | path to observations file                                               |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 4      |:ref:`Transmitters File<aem_input_inv2_ln4>`                  | path to transmitters file                                               |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 5      |:ref:`Receivers File<aem_input_inv2_ln5>`                     | path to receivers file                                                  |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 6      |:ref:`Frequencies File<aem_input_inv2_ln6>`                   | path to frequencies file                                                |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 7      |:ref:`Initial/FWD Model<aem_input_inv2_ln7>`                  | initial model/forward model                                             |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 8      |:ref:`Reference Model<aem_input_inv2_ln8>`                    | reference model                                                         |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 9      |:ref:`Active Topography Cells<aem_input_inv2_ln9>`            | topography                                                              |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 10     |:ref:`Active Model Cells<aem_input_inv2_ln10>`                | active model cells                                                      |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 11     |:ref:`Cell Weights<aem_input_inv2_ln11>`                      | additional cell weights                                                 |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 12     |:ref:`Face Weights<aem_input_inv2_ln12>`                      | additional face weights                                                 |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 13     |:ref:`Norm Sparseness<aem_input_inv2_ln13>`                   | set parameters to recover smooth, sparse or blocky models               |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 14     |:ref:`beta_max beta_min beta_factor<aem_input_inv2_ln14>`     | cooling schedule for beta parameter                                     |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 15     |:ref:`alpha_s alpha_x alpha_y alpha_z<aem_input_inv2_ln15>`   | weighting constants for smallness and smoothness constraints            |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 16     |:ref:`Chi Factor<aem_input_inv2_ln16>`                        | stopping criteria for inversion                                         |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 17     |:ref:`iter_per_beta nBetas<aem_input_inv2_ln17>`              | set the number of Gauss-Newton iteration for each beta value            |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 18     |:ref:`tol_ipcg max_iter_ipcg<aem_input_inv2_ln18>`            | set the tolerance and number of iterations for Gauss-Newton solve       |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 19     |:ref:`Reference Model Update<aem_input_inv2_ln19>`            | reference model                                                         |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 20     |:ref:`Hard Constraints<aem_input_inv2_ln20>`                  | use *SMOOTH_MOD* or *SMOOTH_MOD_DIFF*                                   |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 21     |:ref:`Bounds<aem_input_inv2_ln21>`                            | upper and lower bounds for recovered model                              |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 22     |:ref:`Calculate sensitivity<aem_input_inv2_ln22>`             | use *CALC_SENS* or *NOT_CALC_SENS*                                      |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 23     |:ref:`Memory Options<aem_input_inv2_ln23>`                    | options for storing factorizations of forward system (RAM vs disk)      |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 24     |:ref:`PCT_FACT<aem_input_inv2_ln24>`                          | percent factor for sensitivity calculation                              |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+
| 25     |:ref:`Tile file<aem_input_inv2_ln25>`                         | option to invert using only subset of tiles                             |
+--------+--------------------------------------------------------------+-------------------------------------------------------------------------+



.. .. figure:: images/aem_inv_input2.png
..      :align: center
..      :width: 700

..      Example input file for the inversion program.


Line Descriptions
^^^^^^^^^^^^^^^^^

.. _aem_input_inv2_ln1:

    - **Inversion Mesh:** file path to the :ref:`inversion (OcTree) mesh file<octreeFile>`

.. _aem_input_inv2_ln2:

    - **Forward Mesh:** file path to the :ref:`forward (OcTree) mesh file<octreeFile>`

.. _aem_input_inv2_ln3:

    - **Observation File:** file path to the :ref:`observed data file<obsFile2>`

.. _aem_input_inv2_ln4:

    - **Transmitter File:** file path to the :ref:`transmitter file<receiverFile>`

.. _aem_input_inv2_ln5:

    - **Receiver File:** file path to the :ref:`receiver file<receiverFile>`

.. _aem_input_inv2_ln6:

    - **Frequencies File:** file path to the :ref:`frequencies file<freqFile>`

.. _aem_input_inv2_ln7:

    - **Initial/FWD Model:** On this line we specify either the starting model for the inversion or the conductivity model for the forward modeling. On this line, there are 3 possible options:

        - If the program is being used to forward model data, the flag 'FWDMODEL' is entered followed by the path to the conductivity model.
        - If the program is being used to invert data, only the path to a conductivity model is required; e.g. inversion is assumed unless otherwise specified.
        - If a homogeneous conductivity value is being used as the starting model for an inversion, the user can enter "VALUE" followed by a space and a numerical value; example "VALUE 0.01".


.. important::

    If data are only being forward modeled, only the :ref:`active topography cells<aem_input_inv2_ln7>` and :ref:`tol_ipcg max_iter_ipcg<aem_input_inv2_ln16>` fields are relevant. **However**, the remaining fields must **not** be empty and must have correct syntax for the code to run.


.. _aem_input_inv2_ln8:

    - **Reference Model:** The user may supply the file path to a reference conductivity model. If a homogeneous conductivity value is being used for all active cells, the user can enter "VALUE" followed by a space and a numerical value; example "VALUE 0.01".


.. _aem_input_inv2_ln9:

    - **Active Topography Cells:** Here, the user can choose to specify the cells which lie below the surface topography. To do this, the user may supply the file path to an active cells model file or type "ALL_ACTIVE". The active cells model has values 1 for cells lying below the surface topography and values 0 for cells lying above.

.. _aem_input_inv2_ln10:

    - **Active Model Cells:** Here, the user can choose to specify the model cells which are active during the inversion. To do this, the user may supply the file path to an active cells model file or type "ALL_ACTIVE". The active cells model has values 1 for cells lying below the surface topography and values 0 for cells lying above. Values for inactive cells are provided by the background conductivity model.

.. _aem_input_inv2_ln11:

    - **Cell Weights:** Here, the user specifies whether cell weights are supplied. If so, the user provides the file path to a :ref:`cell weights file <weightsFile>`  If no additional cell weights are supplied, the user enters "NO_WEIGHT".

.. _aem_input_inv2_ln12:

    - **Face Weights:** Here, the user specifies whether face weights are supplied. If so, the user provides the file path to a face weights file :ref:`cell weights file <weightsFile>`. If no additional cell weights are supplied, the user enters "NO_FACE_WEIGHT". The user may also enter "EKBLOM" for 1-norm approximation to recover sharper edges.

.. _aem_input_inv2_ln13:

    - **Sparseness:** The sparseness of the recovered model is determined by the terms within the `model objective function <http://giftoolscookbook.readthedocs.io/en/latest/content/fundamentals/Norms.html>`__ . A standard approach is to use an L2-norm for all terms

        - To use the L2-norm, enter the flag 'USE_L2'
        - To specify the Ekblom norm, enter the flag 'USE_EKBLOM' followed by values for :math:`p` and :math:`\varepsilon` where the Ekblom norm is given by:


.. math::
    \sum_{i=1}^M \, (\sigma_i^2 + \varepsilon^2)^{p/2} \;\;\; \textrm{s.t.} \;\;\; 1\leq p \leq 2, \; \varepsilon > 0



.. _aem_input_inv2_ln14:

    - **beta_max beta_min beta_factor:** Here, the user specifies protocols for the trade-off parameter (beta). *beta_max* is the initial value of beta. *beta_min* is generally used to denote the minimum allowable trade-off parameter the program can use before quitting. For this code however, the minimum beta is determined through the *nBeta* parameter on :ref:`line 15 <aem_input_inv2_ln15>` and the *beta_min* parameter has no function. *beta_factor* defines the factor by which beta is decreased at each iteration; example "1E4 10 0.2". The user may also enter "DEFAULT" if they wish to have beta calculated automatically. See theory on :ref:`cooling schedule <theory_cooling>`.

.. _aem_input_inv2_ln15:

    - **alpha_s alpha_x alpha_y alpha_z:** `Alpha parameters <http://giftoolscookbook.readthedocs.io/en/latest/content/fundamentals/Alphas.html>`__ . Here, the user specifies the relative weighting between the smallness and smoothness component penalties on the recovered models.

.. _aem_input_inv2_ln16:

    - **Chi Factor:** The chi factor defines the target misfit for the inversion. A chi factor of 1 means the target misfit is equal to the total number of data observations. For more, see the `GIFtools cookbook <http://giftoolscookbook.readthedocs.io/en/latest/content/fundamentals/Beta.html>`__ .

.. _aem_input_inv2_ln17:

    - **iter_per_beta nBetas:** Here, *iter_per_beta* is the number of Gauss-Newton iterations per beta value. *nBetas* is the number of times the inverse problem is solved for smaller and smaller trade-off parameters until it quits. See theory section for :ref:`cooling schedule <theory_cooling>` and :ref:`Gauss-Newton update <theory_GN>`.

.. _aem_input_inv2_ln18:

    - **tol_ipcg max_iter_ipcg:** Here, the user specifies solver parameters. *tol_ipcg* defines how well the iterative solver does when solving for :math:`\delta m` and *max_iter_ipcg* is the maximum iterations of incomplete-preconditioned-conjugate gradient. See theory on :ref:`Gauss-Newton solve <theory_IPCG>`

.. _aem_input_inv2_ln19:

    - **Reference Model Update:** Here, the user specifies whether the reference model is updated at each inversion step result. If so, enter "CHANGE_MREF". If not, enter "NOT_CHANGE_MREF".

.. _aem_input_inv2_ln20:

    - **Hard Constraints:** SMOOTH_MOD runs the inversion without implementing a reference model (essential :math:`m_{ref}=0`). "SMOOTH_MOD_DIF" constrains the inversion in the smallness and smoothness terms using a reference model.

.. _aem_input_inv2_ln21:

    - **Bounds:** Bound constraints on the recovered model. Choose "BOUNDS_CONST" and enter the values of the minimum and maximum model conductivity; example "BOUNDS_CONST 1E-6 0.1". Enter "BOUNDS_NONE" if the inversion is unbounded, or if there is no a-prior information about the subsurface model.

.. _aem_input_inv2_ln22:

    - **Calculate sensitivity:** Use the flag *CALC_SENS* to calculate the full sensitivity matrix. Use the flag *NOT_CALC_SENS* to approximate using a set of .

.. _aem_input_inv2_ln23:

    - **Memory Options:** This code uses a factorization to solve the forward system at each frequency. These factorizations must be stored. By using the flag 'FACTOR_IC' (in cpu), factorizations are stored within a computer's RAM. Although this is faster, larger problems cannot be solved if insufficient temporary memory is available. The factorizations are stored in permanent memory (disk) if the flag 'FACTOR_OOC' (out of cpu) is used followed by the path to a directory. This is slower because the program must read these files many times. The second options is ill-advised if files are being transferred over a network.


.. _aem_input_inv2_ln24:

    - **PCT_FACT:** percentage of tiles (local meshes) for which the sensitivities will be calculated (use 1 for airborne). **MORE DETAILS NEEDED**

.. _aem_input_inv2_ln25:

    - **Tile file:** USE_ALL_TILES
