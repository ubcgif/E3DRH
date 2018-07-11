.. _e3dmt_input_fwd:

Forward Modeling Input File
===========================

Version 1 (2014 and 2015)
-------------------------

The forward problem is solved using the executable program **e3dMTfwd.exe**. Parameters necessary for running the forward modeling code are set in the input file. The lines of input file are as follows:

.. tabularcolumns:: |L|C|C|

+--------+------------------------------------------------------+-----------------------------------------------+
| Line # | Parameter                                            | Description                                   |
+========+======================================================+===============================================+
|   1    |:ref:`OcTree Mesh<e3dmt_input_fwd_ln1>`               | path to octree mesh file                      |
+--------+------------------------------------------------------+-----------------------------------------------+
|   2    |:ref:`Receiver Locations<e3dmt_input_fwd_ln2>`        | path to observation locations file            |
+--------+------------------------------------------------------+-----------------------------------------------+
|   3    |:ref:`Real Conductivity<e3dmt_input_fwd_ln3>`         | path to conductivity model                    |
+--------+------------------------------------------------------+-----------------------------------------------+
|   4    |:ref:`Imaginary Conductivity<e3dmt_input_fwd_ln4>`    | path to imaginary conductivity file (optional)|
+--------+------------------------------------------------------+-----------------------------------------------+
|   5    |:ref:`1D Background Conductivity<e3dmt_input_fwd_ln5>`| set 1D conductivity model                     |
+--------+------------------------------------------------------+-----------------------------------------------+
|   6    |:ref:`Background Susceptibility<e3dmt_input_fwd_ln6>` | set background susceptibility                 |
+--------+------------------------------------------------------+-----------------------------------------------+
|   7    |:ref:`Topography<e3dmt_input_fwd_ln7>`                | set topography                                |
+--------+------------------------------------------------------+-----------------------------------------------+




.. figure:: images/create_fwd_input.png
     :align: center
     :width: 700

     Example input file for forward modeling program (`Download <https://github.com/ubcgif/e3dmt/raw/master/assets/input_files1/e3dMT_octree_fwd.inp>`__ ).


Line Descriptions
^^^^^^^^^^^^^^^^^

.. _e3dmt_input_fwd_ln1:

    - **OcTree Mesh:** file path to the OcTree mesh file

.. _e3dmt_input_fwd_ln2:

    - **Receiver Locations:** file path to the :ref:`survey file<surveyFile>`.

.. _e3dmt_input_fwd_ln3:

    - **Real Conductivity:** file path to the conductivity model. If complex conductivities are being used, this model represents real-valued conductivities.

.. _e3dmt_input_fwd_ln4:

    - **Imaginary Conductivity:** If the conductivity model used in the forward simulation is strictly real-valued, the user may enter "NO_IMAG_COND" on this line. Otherwise, the user enters the file path to the imaginary conductivity model.

.. _e3dmt_input_fwd_ln5:

    - **1D Background Conductivity:** The user may supply the file path to a `1D background conductivity model <http://em1dfm.readthedocs.io/en/latest/content/files/supporting.html#files-for-reference-and-starting-models>`__ . If a homogeneous background conductivity is being used, the user enters "VALUE" followed by a space and a numerical value; example "VALUE 0.01"

.. _e3dmt_input_fwd_ln6:

    - **Background Susceptibility:** The user may provide the file path to a background susceptibility model on this line. If a constant susceptibility is being used, "VALUE" may be entered and followed by the background susceptibility. For no background susceptibility, the flag "NO_SUS" is used.

.. _e3dmt_input_fwd_ln7:

    - **Topography:** The user may supply the file path to an active cells model file or type "ALL_ACTIVE". The active cells model has values 1 for cells lying below the surface topography and values 0 for cells lying above.


Version 2 (2017)
----------------

Both the forward problem and inverse problem are solved using the executable program **e3dMTinv_ver2.exe**. As a result, the :ref:`input file<e3dmt_input_inv2>` will be described within the :ref:`running the inversion<e3dmt_inv2>` section.



