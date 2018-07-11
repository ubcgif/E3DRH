.. _indexFile:

Survey Index File
=================

.. important:: Only relevant to the E3DMT version 2 (2017) code.

This file is used to define the locations at which MT and ZTEM data are predicted. Each row of the survey index file is used to index the electric dipole and inductive loop receivers corresponding to a specific set of impedance tensor or Z-axis tipper measurements. This file is required for both forward modeling. The indicies correspond to receivers defined within the :ref:`receiver file<receiverFile>`. The user also defines the data type being modeled. The lines of the survey index file depend on whether MT or ZTEM are being modeled.

Format
------

.. note::
    - Bolded entries are fixed flags recognized by the Fortran codes and blue hyperlinked entries are values/regular expressions specified by the user


MT Data
^^^^^^^

| **DATATYPE MT**
| :ref:`f_ind<e3dmt_ind_ln1>` :math:`\;` :ref:`Ex_ind<e3dmt_ind_ln2>` :math:`\;` :ref:`Ey_ind<e3dmt_ind_ln3>` :math:`\;` :ref:`Hx_ind<e3dmt_ind_ln4>` :math:`\;` :ref:`Hy_ind<e3dmt_ind_ln5>` :math:`\;` :ref:`1<e3dmt_ind_ln7>`
| :ref:`f_ind<e3dmt_ind_ln1>` :math:`\;` :ref:`Ex_ind<e3dmt_ind_ln2>` :math:`\;` :ref:`Ey_ind<e3dmt_ind_ln3>` :math:`\;` :ref:`Hx_ind<e3dmt_ind_ln4>` :math:`\;` :ref:`Hy_ind<e3dmt_ind_ln5>` :math:`\;` :ref:`1<e3dmt_ind_ln7>`
| :ref:`f_ind<e3dmt_ind_ln1>` :math:`\;` :ref:`Ex_ind<e3dmt_ind_ln2>` :math:`\;` :ref:`Ey_ind<e3dmt_ind_ln3>` :math:`\;` :ref:`Hx_ind<e3dmt_ind_ln4>` :math:`\;` :ref:`Hy_ind<e3dmt_ind_ln5>` :math:`\;` :ref:`1<e3dmt_ind_ln7>`
| :math:`\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\; \vdots`
| :ref:`f_ind<e3dmt_ind_ln1>` :math:`\;` :ref:`Ex_ind<e3dmt_ind_ln2>` :math:`\;` :ref:`Ey_ind<e3dmt_ind_ln3>` :math:`\;` :ref:`Hx_ind<e3dmt_ind_ln4>` :math:`\;` :ref:`Hy_ind<e3dmt_ind_ln5>` :math:`\;` :ref:`1<e3dmt_ind_ln7>`
|
|


Below we show an example of a survey index file for MT data. In this case, the impedance tensor data are modeled at 3 frequencies and a new set of receivers is used at each measurement site.

.. figure:: images/mtindex_file.png
     :align: center
     :width: 700

     Survey index file for MT data.


.. important::

    - The frequency indicies in row 1 cannot decrease in value; e.g. you cannot have a row which starts with 3 followed by a row that starts with 2.
    - The number of rows and receiver indicies for measurements at a given frequency do not need to match those for another frequency; e.g. you can have 50 stations taking measurements at 1 Hz and 65 completely different stations taking measurements at 10 Hz.

ZTEM Data
^^^^^^^^^

| **DATATYPE ZTEM**
| :ref:`f_ind<e3dmt_ind_ln1>` :math:`\;` :ref:`Hx_ind<e3dmt_ind_ln4>` :math:`\;` :ref:`Hy_ind<e3dmt_ind_ln5>` :math:`\;` :ref:`Hz_ind<e3dmt_ind_ln6>` :math:`\;` :ref:`1<e3dmt_ind_ln7>`
| :ref:`f_ind<e3dmt_ind_ln1>` :math:`\;` :ref:`Hx_ind<e3dmt_ind_ln4>` :math:`\;` :ref:`Hy_ind<e3dmt_ind_ln5>` :math:`\;` :ref:`Hz_ind<e3dmt_ind_ln6>` :math:`\;` :ref:`1<e3dmt_ind_ln7>`
| :ref:`f_ind<e3dmt_ind_ln1>` :math:`\;` :ref:`Hx_ind<e3dmt_ind_ln4>` :math:`\;` :ref:`Hy_ind<e3dmt_ind_ln5>` :math:`\;` :ref:`Hz_ind<e3dmt_ind_ln6>` :math:`\;` :ref:`1<e3dmt_ind_ln7>`
| :math:`\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\; \vdots`
| :ref:`f_ind<e3dmt_ind_ln1>` :math:`\;` :ref:`Hx_ind<e3dmt_ind_ln4>` :math:`\;` :ref:`Hy_ind<e3dmt_ind_ln5>` :math:`\;` :ref:`Hz_ind<e3dmt_ind_ln6>` :math:`\;` :ref:`1<e3dmt_ind_ln7>`
|
|

Below we show an example of a survey index file for ZTEM data. In this case, the tipper data are modeled at 3 frequencies and the same receiver is used to measure Hx and Hy at all measurement sites.


.. figure:: images/ztemindex_file.png
     :align: center
     :width: 700

     Survey index file for ZTEM data.


.. important::

    - The frequency indicies in row 1 cannot decrease in value; e.g. you cannot have a row which starts with 3 followed by a row that starts with 2.
    - The number of rows and receiver indicies for measurements at a given frequency do not need to match those for another frequency; e.g. you can have 50 stations taking measurements at 1 Hz and 65 completely different stations taking measurements at 10 Hz.


Parameter Descriptions
----------------------


.. _e3dmt_ind_ln1:

    - **f_ind:** The index corresponding to the desired frequency within the :ref:`frequencies file<freqFile>`. 

.. _e3dmt_ind_ln2:

    - **Ex_ind:** The index corresponding to the desired receiver within the :ref:`receiver file<receiverFile>` that measures Ex.

.. _e3dmt_ind_ln3:

    - **Ey_ind:** The index corresponding to the desired receiver within the :ref:`receiver file<receiverFile>` that measures Ey.

.. _e3dmt_ind_ln4:

    - **Hx_ind:** The index corresponding to the desired receiver within the :ref:`receiver file<receiverFile>` that measures Hx.

.. _e3dmt_ind_ln5:

    - **Hy_ind:** The index corresponding to the desired receiver within the :ref:`receiver file<receiverFile>` that measures Hy.

.. _e3dmt_ind_ln6:

    - **Hz_ind:** The index corresponding to the desired receiver within the :ref:`receiver file<receiverFile>` that measures Hz.

.. _e3dmt_ind_ln7:

    - **1:** As of May 2018, a flag value of 1 is entered here. In future iterations of the code, this entry may be related to additional functionality.




















