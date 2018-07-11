.. _preFile:

Predicted Data File
===================


Version 1 (2014 and 2015)
-------------------------

The predicted data file is output from **e3dMTfwd.exe** and contains the locations and predicted data. The order of the data point is in the same order as the :ref:`survey and locations file <surveyFile>`. Each block, separated by a blank line, are the data for a particular transmitter and frequency. Thus predicted data files take the format:

|
| **Data Array 1**
|
| **Data Array 2**
|
| :math:`\;\;\;\;\;\;\;\; \vdots`
|
| **Data Array N**
|
|



MT data (DATATYPE = MTZ)
^^^^^^^^^^^^^^^^^^^^^^^^

Each row in the array contains the elements of the impedance tensor at a particular location separated into real and imaginary components. The units for predicted MT data are (V/A). The columns for this data format are as follows:

.. math::
    | \; x \; | \; y \; | \; z \; | \; Z^\prime_{11} \; | \; Z^{\prime \prime}_{11} \; | \; Z^\prime_{12} \; | \; Z^{\prime \prime}_{12} \; | \; Z^\prime_{21} \; | \; Z^{\prime \prime}_{21} \; | \; Z^\prime_{22} \; | \; Z^{\prime \prime}_{22} \; |

where

    - The coordinates are right-handed with X (Easting), Y (Northing) and Z+ (Up)
    - :math:`Z^\prime_{ij}` is the real component of entry i,j of the impedance tensor
    - :math:`Z^{\prime\prime}_{ij}` is the imaginary component of entry i,j of the impedance tensor


ZTEM data (DATATYPE = MTT, MTE or MTH)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Each row in the array contains the elements of the transfer function at a particular location separated into real and imaginary components. Predicted ZTEM data are unitless with no normalization factor. The columns for this data format are as follows:

.. math::
    | \; x \; | \; y \; | \; z \; | \; T^\prime_x \; | \; T^{\prime \prime}_x \; | \; T^\prime_y \; | \; T^{\prime \prime}_y \; |

where

    - The coordinates are right-handed with X (Easting), Y (Northing) and Z+ (Up)
    - :math:`T^\prime_x` is the real component of :math:`T_x`
    - :math:`T^{\prime\prime}_x` is the imaginary component of :math:`T_x`

and similarly for :math:`y`.


Version 2 (2017)
----------------

Predicted data files output by **e3dMTinv_ver2.exe** contain the locations and predicted data. The ordering (rows) of the data correspond to the rows in the :ref:`index file <indexFile>`. For plotting purposes, the predicted data are defined at a single point; despite the fact that raw fields are measured with a set of receivers. This point depends on the locations of the receivers at for each measurement location and is different for MT and ZTEM data.


MT data (DATATYPE MT)
^^^^^^^^^^^^^^^^^^^^^

Each row in the array contains the elements of the impedance tensor, defined at a particular location and separated into real and imaginary components. The units for predicted MT data are (V/A). The rows for this data format are as follows:

.. math::
    | \; x \; | \; y \; | \; z \; | \; Z^\prime_{11} \; | \; Z^{\prime \prime}_{11} \; | \; Z^\prime_{12} \; | \; Z^{\prime \prime}_{12} \; | \; Z^\prime_{21} \; | \; Z^{\prime \prime}_{21} \; | \; Z^\prime_{22} \; | \; Z^{\prime \prime}_{22} \; |

where

    - The coordinates are right-handed with X (Easting), Y (Northing) and Z+ (Up)
    - :math:`Z^\prime_{ij}` is the real component of entry i,j of the impedance tensor
    - :math:`Z^{\prime\prime}_{ij}` is the imaginary component of entry i,j of the impedance tensor

.. important::

    - The x, y, z location is the average of the node locations defining the Hy receiver. Thus if the same Hy receiver is used for several measurements, the data will be plotted in the same location.


ZTEM data (DATATYPE ZTEM)
^^^^^^^^^^^^^^^^^^^^^^^^^

Each row in the array contains the elements of the transfer function, defined at a particular location and separated into real and imaginary components. Predicted ZTEM data are unitless with no normalization factor. The rows for this data format are as follows:

.. math::
    | \; x \; | \; y \; | \; z \; | \; T^\prime_x \; | \; T^{\prime \prime}_x \; | \; T^\prime_y \; | \; T^{\prime \prime}_y \; |

where

    - The coordinates are right-handed with X (Easting), Y (Northing) and Z+ (Up)
    - :math:`T^\prime_x` is the real component of :math:`T_x`
    - :math:`T^{\prime\prime}_x` is the imaginary component of :math:`T_x`

and similarly for :math:`y`.

.. important::

    - The x, y, z location is the average of the node locations defining the Hz receiver. Thus if the same Hz receiver is used for several measurements, the data will be plotted in the same location.













