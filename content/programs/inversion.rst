.. _e3d_inv:

Inversion Program
=================

Both the forward and inverse problems are solved using the **e3d_v2_tiled.exe** executable program. In each case, format of the :ref:`input file<e3d_input_inv>` (denoted here as **e3dinv.inp**) is the same. In the case of forward modeling however, some lines in the input file are omitted.

Running the Program
^^^^^^^^^^^^^^^^^^^

Here, the *mpiexec* call is used to parallelize multiple processes (large-scale independent operations) within the code. To run the executable, open a command window and type the following:

.. figure:: images/run_e3dinv_ver2_tiled.png
     :align: center
     :width: 500


The call *mpiexec* is followed by the flag *-n*, then the number of processes (*"nFreq"* ) to be carried out simultaneously. This is followed by the paths to the executable and the corresponding input file, respectively. The number of simultaneous processes (*"nFreq"* ) **must** be equal or less than the number of frequencies. Ideally there is enough memory for *nFreq* to be equal to the number of frequencies.

Setting Number of Threads with Open MPI
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Before running the executable, the number of threads used to carry out all simultaneous processes can be set with Open MPI. This is set in the command window **before** running the executable. To set the number of threads (*nThreads* ), use the following syntax:

    - Windows computer: "set OMP_NUM_THREADS=nThreads"
    - Linux (bash shell): "export OMP_NUM_THREADS=nThreads"
    - Linux (csh shell): "setenv OMP_NUM_THREADS nThreads"

.. important:: The number of processes (*nFreq* ) times the number of threads (*nThreads* ) **cannot** exceed the total number of threads available from the computer.

Units
^^^^^

**Input and outputs:**

    - **Magnetic field data:** the component of the total magnetic field along the direction of the receiver's dipole moment in units A/m
    - **Electric field data:** the component of the electric field along the path of the wire segment
    - **Conductivity model:** S/m
    - **Reference/starting conductivity model:** S/m 
    - **Model/interface weights:** unitless


.. important::

    - If a flag value of -99 is used as the uncertainty for a particular datum, the inversion will omit that datum. Using this, we are not required to invert all of the data.


Output Files
^^^^^^^^^^^^

**THIS IS NOT CORRECT**

The program **e3d_v2_tiled.exe** creates the following output files:

    - **inv.con:** recovered conductivity model for the final beta value

    - **inv_n.con:** recovered conductivity model for the nth beta value

    - **dpred0.txt** predicted data for the initial model

    - **dpredn.txt** predicted data for the nth beta value

    - **dpred.txt** predicted data for final recovered model

    - **e3d_v2_tiled.log:** log file for the inversion

    - **e3d_v2_tiled.out:** inversion summary





