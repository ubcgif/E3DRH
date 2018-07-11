.. _obsFile:

Observations File
=================

This file is input when inverting field-collected data. This file contains the survey information, field observations and data uncertainties. 

Version 1 (2014 and 2015)
-------------------------

.. important:: As of May 2018, the user must invert all 4 components of the impedance tensor for MT data OR both components of the transfer function for ZTEM data. Also, flags cannot be used to omit data points.

Format
^^^^^^

.. note::
    - Bolded entries are fixed flags recognized by the Fortran codes and blue hyperlinked entries are values/regular expressions specified by the user
    - Each unique data type, frequency and set of observation locations corresponds to a unique "transmitter"; e.g. 2 transmitters must be specified if the same data are collected at the same locations at 2 different frequencies.
    - Each block contains DATATYPE, FREQUENCY, N_RECV and the data array


The lines of a data file with one or more transmitters are formatted as follows:

| **N_TRX** :math:`\;` :ref:`A<e3dmt_obs_ln1>`
| **!IGNORE** :math:`\;` :ref:`B<e3dmt_obs_ln2>`
|
| **DATATYPE** :math:`\;` :ref:`C<e3dmt_obs_ln3>`
| **FREQUENCY** :math:`\;` :ref:`D<e3dmt_obs_ln4>`
| **N_RECV** :math:`\;` :ref:`E<e3dmt_obs_ln5>`
| :ref:`Data Array<e3dmt_obs_ln6>`
|
| **DATATYPE** :math:`\;` :ref:`C<e3dmt_obs_ln3>`
| **FREQUENCY** :math:`\;` :ref:`D<e3dmt_obs_ln4>`
| **N_RECV** :math:`\;` :ref:`E<e3dmt_obs_ln5>`
| :ref:`Data Array<e3dmt_obs_ln6>`
|
| :math:`\;\;\;\;\;\;\;\; \vdots`
|
| **DATATYPE** :math:`\;` :ref:`C<e3dmt_obs_ln3>`
| **FREQUENCY** :math:`\;` :ref:`D<e3dmt_obs_ln4>`
| **N_RECV** :math:`\;` :ref:`E<e3dmt_obs_ln5>`
| :ref:`Data Array<e3dmt_obs_ln6>`
|
|


.. figure:: images/files_data.png
     :align: center
     :width: 700

     Example data file for MTZ data.


Parameter Descriptions
^^^^^^^^^^^^^^^^^^^^^^


.. _e3dmt_obs_ln1:

    - **(A) Number of transmitters:** In line 1, the number of transmitters/groups of natural source EM data is specified. Example: *N_TRX 3*

.. _e3dmt_obs_ln2:

    - **(B) Flag to ignore data entries:** A regular expression is entered, signifying data in the data structure which is ignored during the inversion. Example: *!IGNORE -0*

.. _e3dmt_obs_ln3:

    - **(C) Data type:**. For the data corresponding to each transmitter, this line sets the type of data. Example: *DATATYPE MTZ*. There are 4 options for DATATYPE:

        - "MTZ" - MT data (Both real and imaginary impedance tensor data)
        - "MTT" - ZTEM data (Hx and Hy constant at first receiver location and first receiver station defines base station)
        - "MTE" - ZTEM data where Hx, Hy are calculated at the base station from the initial model
        - "MTH" - ZTEM data (reference is at the data points - no base station)

.. important::

    - When modeling MT and ZTEM data simultaneously, you must choose either type MTZ and MTT or MT and MTE or MTZ and MTH; e.g. you cannot have MTT, MTE and MTH in the same observations file.
        
.. _e3dmt_obs_ln4:

    - **(D) Frequency:** Frequency at which the corresponding set of field observations are made. Example: *FREQUENCY 1.0000E+002*.

.. _e3dmt_obs_ln5:

    - **(E) Number of receivers:** Number of receivers collecting data at the aforementioned frequency for the aforementioned data type. Example: *N_RECV 900*.

.. _e3dmt_obs_ln6:

    - **Data Array:** Contains the locations and field observations for the data specified by :ref:`data type<e3dmt_obs_ln3>`. The number of lines in this array is equal to the number of receivers. The number of columns depends on the type of data specified. The columns for defined for each array are show :ref:`below<obsFile_data>`.


.. _obsFile_data:

Data Arrays by Type
^^^^^^^^^^^^^^^^^^^

**MT data (DATATYPE = MTZ):**

Each row in the array contains the elements of the impedance tensor at a particular location separated into real and imaginary components, along with the corresponding uncertainties. The units for MT data are (V/A). The columns for this data format are as follows:

.. math::
    | \; x \; | \; y \; | \; z \; | \;\;\; Z_{11} \; data \;\;\; | \;\;\; Z_{12} \; data \;\;\; | \;\;\; Z_{21} \; data \;\;\; | \;\;\; Z_{22} \; data \;\;\; |

such that each :math:`Z_{ij} \; data` is comprised of 4 columns:

.. math::

    | \; Z^\prime_{ij} \; | \; U^\prime_{ij} \; | \; Z^{\prime \prime}_{ij} \; | \; U^{\prime \prime}_{ij} \; |

where

    - :math:`Z^\prime_{ij}` is the real component of entry i,j of the impedance tensor
    - :math:`Z^{\prime\prime}_{ij}` is the imaginary component of entry i,j of the impedance tensor
    - :math:`U^\prime_{ij}` is the uncertainty on :math:`Z^\prime_{ij}`
    - :math:`U^{\prime\prime}_{ij}` is the uncertainty on :math:`Z^{\prime\prime}_{ij}`


**ZTEM data (DATATYPE = MTT, MTE or MTH):**

Each row in the array contains the elements of the transfer function at a particular location separated into real and imaginary components, along with the corresponding uncertainties. Data values and uncertainties are unitless with no normalization factor. The columns for this data format are as follows:

.. math::
    | \; x \; | \; y \; | \; z \; | \;\;\; T_x \; data \;\;\; | \;\;\; T_y \; data \;\;\; |

such that each :math:`T_x \; data` is comprised of 4 columns:

.. math::

    | \; T^\prime_x \; | \; U^\prime_x \; | \; T^{\prime \prime}_x \; | \; U^{\prime \prime}_x \; |

where

    - :math:`T^\prime_x` is the real component of :math:`T_x`
    - :math:`T^{\prime\prime}_x` is the imaginary component of :math:`T_x`
    - :math:`U^\prime_x` is the uncertainty on :math:`T^\prime_x`
    - :math:`U^{\prime\prime}_x` is the uncertainty on :math:`T^{\prime\prime}_x`

and similarly for :math:`y`.


.. important::

    - If MT and/or ZTEM data are being modeled, the frequencies do not need to match nor do the locations for each frequency.
    - For **MTT and MTE data (ZTEM)**, the first line in the array refers to the base/reference station location. Only the x,y and z locations are required. **However**, each remaining field must be given a flag value of "i". *Example for first row:* :math:`350 \;\; 200 \;\; 0 \;\; i \;\; i \;\; i \;\; i \;\; i \;\; i \;\; i \;\; i`
    - For **MTH data (ZTEM)**, measurements Hx, Hy and Hz are taken at different locations. Data and uncertainty values are required for all rows.
    - For **MTT and MTE data (ZTEM)**, the first line in the array refers to the base/reference station location. Thus if there are :math:`N` receiver locations specified for a given array with data type "MTT", the inversion will output :math:`N-1` rows of predicted data in the predicted data files.
    - For **MTH data (ZTEM)**, measurements Hx, Hy and Hz are taken at the same location. Thus if there are :math:`N` receiver locations specified for a given array with data type "MTH", the inversion model will output :math:`N` rows of predicted data in the predicted data files.


.. _obsFile2:

Version 2 (2017)
----------------

.. important::

    - As of May 2018, the E3DMT version 2 code cannot simultaneously invert both MT and ZTEM data, just one or the other.
    - If a flag value of '-99' is entered as an uncertainty, the corresponding data value is not fit during the inversion. Therefore, we can omit inverting the diagonal elements of the impedance tensor.

MT Data Format
^^^^^^^^^^^^^^

.. note:: Blue hyperlinked entries are values/regular expressions specified by the user

The format of the observation file for MT data begins by defining the datatype flag on the first line. The frequency index, receiver indicies, observed data and uncertainties are then defined on each subsequent line.


| **DATATYPE MT**
| :ref:`f_ind<e3dmt_obs2_ln1>` :math:`\;` :ref:`Ex_ind<e3dmt_obs2_ln2>` :math:`\;` :ref:`Ey_ind<e3dmt_obs2_ln3>` :math:`\;` :ref:`Hx_ind<e3dmt_obs2_ln4>` :math:`\;` :ref:`Hy_ind<e3dmt_obs2_ln5>` :math:`\;` :ref:`1<e3dmt_obs2_ln7>` :math:`\; [Z_{11} \; data] \; [Z_{12} \; data] \; [Z_{21} \; data] \; [Z_{22} \; data]`
| :ref:`f_ind<e3dmt_obs2_ln1>` :math:`\;` :ref:`Ex_ind<e3dmt_obs2_ln2>` :math:`\;` :ref:`Ey_ind<e3dmt_obs2_ln3>` :math:`\;` :ref:`Hx_ind<e3dmt_obs2_ln4>` :math:`\;` :ref:`Hy_ind<e3dmt_obs2_ln5>` :math:`\;` :ref:`1<e3dmt_obs2_ln7>` :math:`\; [Z_{11} \; data] \; [Z_{12} \; data] \; [Z_{21} \; data] \; [Z_{22} \; data]`
| :ref:`f_ind<e3dmt_obs2_ln1>` :math:`\;` :ref:`Ex_ind<e3dmt_obs2_ln2>` :math:`\;` :ref:`Ey_ind<e3dmt_obs2_ln3>` :math:`\;` :ref:`Hx_ind<e3dmt_obs2_ln4>` :math:`\;` :ref:`Hy_ind<e3dmt_obs2_ln5>` :math:`\;` :ref:`1<e3dmt_obs2_ln7>` :math:`\; [Z_{11} \; data] \; [Z_{12} \; data] \; [Z_{21} \; data] \; [Z_{22} \; data]`
| :math:`\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\; \vdots`
| :ref:`f_ind<e3dmt_obs2_ln1>` :math:`\;` :ref:`Ex_ind<e3dmt_obs2_ln2>` :math:`\;` :ref:`Ey_ind<e3dmt_obs2_ln3>` :math:`\;` :ref:`Hx_ind<e3dmt_obs2_ln4>` :math:`\;` :ref:`Hy_ind<e3dmt_obs2_ln5>` :math:`\;` :ref:`1<e3dmt_obs2_ln7>` :math:`\; [Z_{11} \; data] \; [Z_{12} \; data] \; [Z_{21} \; data] \; [Z_{22} \; data]`
|
|

such that each :math:`[Z_{ij} \; data]` is comprised of 4 columns:

.. math::

    | \; Z^\prime_{ij} \; | \; U^\prime_{ij} \; | \; Z^{\prime \prime}_{ij} \; | \; U^{\prime \prime}_{ij} \; |

where

    - :math:`Z^\prime_{ij}` is the real component of entry i,j of the impedance tensor
    - :math:`Z^{\prime\prime}_{ij}` is the imaginary component of entry i,j of the impedance tensor
    - :math:`U^\prime_{ij}` is the uncertainty on :math:`Z^\prime_{ij}`
    - :math:`U^{\prime\prime}_{ij}` is the uncertainty on :math:`Z^{\prime\prime}_{ij}`



Below we show an example of a survey index file for MT data.

.. figure:: images/dobs2.png
     :align: center
     :width: 700

     Observed data file for MT data.

ZTEM Data Format
^^^^^^^^^^^^^^^^

The format of the observation file for ZTEM data begins by defining the datatype flag on the first line. The frequency index, receiver indicies, observed data and uncertainties are then defined on each subsequent line.


| **DATATYPE ZTEM**
| :ref:`f_ind<e3dmt_obs2_ln1>` :math:`\;` :ref:`Hx_ind<e3dmt_obs2_ln4>` :math:`\;` :ref:`Hy_ind<e3dmt_obs2_ln5>` :math:`\;` :ref:`Hz_ind<e3dmt_obs2_ln6>` :math:`\;` :ref:`1<e3dmt_obs2_ln7>` :math:`\; [T_x \; data] \; [T_y \; data]`
| :ref:`f_ind<e3dmt_obs2_ln1>` :math:`\;` :ref:`Hx_ind<e3dmt_obs2_ln4>` :math:`\;` :ref:`Hy_ind<e3dmt_obs2_ln5>` :math:`\;` :ref:`Hz_ind<e3dmt_obs2_ln6>` :math:`\;` :ref:`1<e3dmt_obs2_ln7>` :math:`\; [T_x \; data] \; [T_y \; data]`
| :ref:`f_ind<e3dmt_obs2_ln1>` :math:`\;` :ref:`Hx_ind<e3dmt_obs2_ln4>` :math:`\;` :ref:`Hy_ind<e3dmt_obs2_ln5>` :math:`\;` :ref:`Hz_ind<e3dmt_obs2_ln6>` :math:`\;` :ref:`1<e3dmt_obs2_ln7>` :math:`\; [T_x \; data] \; [T_y \; data]`
| :math:`\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\; \vdots`
| :ref:`f_ind<e3dmt_obs2_ln1>` :math:`\;` :ref:`Hx_ind<e3dmt_obs2_ln4>` :math:`\;` :ref:`Hy_ind<e3dmt_obs2_ln5>` :math:`\;` :ref:`Hz_ind<e3dmt_obs2_ln6>` :math:`\;` :ref:`1<e3dmt_obs2_ln7>` :math:`\; [T_x \; data] \; [T_y \; data]`
|
|


such that each :math:`T_x \; data` is comprised of 4 columns:

.. math::

    | \; T^\prime_x \; | \; U^\prime_x \; | \; T^{\prime \prime}_x \; | \; U^{\prime \prime}_x \; |

where

    - :math:`T^\prime_x` is the real component of :math:`T_x`
    - :math:`T^{\prime\prime}_x` is the imaginary component of :math:`T_x`
    - :math:`U^\prime_x` is the uncertainty on :math:`T^\prime_x`
    - :math:`U^{\prime\prime}_x` is the uncertainty on :math:`T^{\prime\prime}_x`

and similarly for :math:`y`.


Parameter Descriptions
^^^^^^^^^^^^^^^^^^^^^^


.. _e3dmt_obs2_ln1:

    - **f_ind:** The index corresponding to the desired frequency within the :ref:`frequencies file<freqFile>`. 

.. _e3dmt_obs2_ln2:

    - **Ex_ind:** The index corresponding to the desired receiver within the :ref:`receiver file<receiverFile>` that measures Ex.

.. _e3dmt_obs2_ln3:

    - **Ey_ind:** The index corresponding to the desired receiver within the :ref:`receiver file<receiverFile>` that measures Ey.

.. _e3dmt_obs2_ln4:

    - **Hx_ind:** The index corresponding to the desired receiver within the :ref:`receiver file<receiverFile>` that measures Hx.

.. _e3dmt_obs2_ln5:

    - **Hy_ind:** The index corresponding to the desired receiver within the :ref:`receiver file<receiverFile>` that measures Hy.

.. _e3dmt_obs2_ln6:

    - **Hz_ind:** The index corresponding to the desired receiver within the :ref:`receiver file<receiverFile>` that measures Hz.

.. _e3dmt_obs2_ln7:

    - **1:** As of May 2018, a flag value of 1 is entered here. In future iterations of the code, this entry may be related to additional functionality.
















