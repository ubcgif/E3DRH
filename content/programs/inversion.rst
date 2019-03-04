.. _e3d_inv:

Inversion Program
=================

Both the forward and inverse problems are solved using the **e3dinv_ver2.exe** executable program. In each case, format of the :ref:`input file<e3d_input_inv>` (denoted here as **e3dinv_ver2.inp**) is the same. In the case of forward modeling however, some lines in the input file are omitted.

Running the Program
^^^^^^^^^^^^^^^^^^^

To run the inversion, open a command line window and type the following:


.. figure:: images/run_e3dinv_ver2.png
     :align: center
     :width: 500


The *mpiexec* call is used for parallelization. This is followed by the flag *-n*, then the number of frequencies (*"nFreq"*). This is followed by the inversion executable and the corresponding input file.

Units
^^^^^

    - **Data:** the component of the total magnetic field along the direction of the receiver's dipole moment in units A/m
    - **Conductivity model:** S/m
    - **Reference/starting conductivity model:** S/m 
    - **Model/interface weights:** unitless


.. important::

    - If a flag value of -99 is used as the uncertainty for a particular datum, the inversion will omit that datum. Using this, we are not required to invert all of the data.


Output Files
^^^^^^^^^^^^

The program **e3dinv_ver2.exe** creates the following output files:

    - **inv.con:** recovered conductivity model for the final beta value

    - **inv_xxx.con:** recovered conductivity model for the nth beta value

    - **dpred0.txt** predicted data for the initial model

    - **dpred_xxx.txt** predicted data for the nth beta value

    - **dpred.txt** predicted data for final recovered model

    - **e3dinv_1mesh.log:** log file for the inversion

    - **e3dinv_1mesh.out:** inversion summary





