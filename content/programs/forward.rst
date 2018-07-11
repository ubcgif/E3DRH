.. _e3dmt_fwd:

Forward Modeling Program
========================

Version 1 (2014 and 2015)
-------------------------

The forward problem is solved using the executable program **e3dMTfwd.exe**. Parameters necessary for running the forward modeling code are set in the :ref:`input file<e3dmt_input_fwd>`; denoted here as **e3dMT_octree_fwd.inp**.

Running the Program
^^^^^^^^^^^^^^^^^^^

To run the forward modeling program, open a command line window. Type the path to the code **e3dMTfwd.exe**, followed by a space, followed by the path to the :ref:`input file<e3dmt_input_fwd>`.

.. figure:: images/run_e3dmt_fwd.png
     :align: center
     :width: 600


Units:
^^^^^^

**Inputs:**

    - **Conductivity model:** S/m
    - **Background susceptibility model:** SI

**Outputs:**

    - **MT data:** Real and imaginary components of impedance tensor entries (V/A)
    - **ZTEM data:** Real and imaginary components of transfer function entries (unitless)


.. _e3dmt_fwd_output:

Output Files
^^^^^^^^^^^^

The program **e3dMTfwd.exe** creates 2 output files:

    - **MT_data.txt:** data predicted using the conductivity model provided

    - **ed3MT_octree_fwd.log:** log file


Version 2 (2017)
----------------

Both the forward problem and inverse problem are solved using the executable program **e3dMTinv_ver2.exe**. As a result, the :ref:`input file<e3dmt_input_inv2>` will be described within the :ref:`running the inversion<e3dmt_inv2>` section.



