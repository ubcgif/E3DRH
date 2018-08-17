.. _aem_inv:

Inversion Program
=================

Both the forward and inverse problems are solved using the **AEM.exe** executable program. In each case, format of the :ref:`input file<aem_input_inv>` (denoted here as **AEM.inp**) is the same. In the case of forward modeling however, some lines in the input file are omitted.

Running the Program
^^^^^^^^^^^^^^^^^^^

To run the inversion, open a command line window and type the following:

**IMAGE NEEDED**

The *mpiexec* call is used for parallelization. This is followed by the flag *-n*, then the number of frequencies (*"nFreq"*). This is followed by the inversion executable and the corresponding input file.

Units
^^^^^

**Input and outputs:**

    - **FEM data:** Real and imaginary components of the auxiliary field H in units A/m
    - **Conductivity model:** S/m
    - **Reference/starting conductivity model:** S/m 
    - **Model/interface weights:** unitless


.. important::

    - If a flag value of -99 is used as the uncertainty for a particular datum, the inversion will omit that datum. Using this, we are not required to invert all of the data.


Output Files
^^^^^^^^^^^^

The program **AEM.exe** creates the following output files:

    - **inv.con:** recovered conductivity model for the final beta value

    - **inv_n.con:** recovered conductivity model for the nth beta value

    - **dpred0.txt** predicted data for the initial model

    - **dpredn.txt** predicted data for the nth beta value

    - **dpred.txt** predicted data for final recovered model

    - **e3d octree inv tiles.log:** log file for the inversion

    - **e3d octree inv tiles.out:** inversion summary





