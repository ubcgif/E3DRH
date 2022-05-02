.. _obsFile:

Observations File
=================

The observations file contains the set of field measurements used in the inversion. This file contains all necessary survey information including: the number of transmitters, transmitter geometry, observation locations, frequencies, observed fields and uncertainties. 

.. note:: Bolded entries are fixed flags recognized by the Fortran codes and blue hyperlinked entries are values/regular expressions specified by the user


The lines the observations file are formatted as follows:



| **IGNORE** :ref:`reg_exp<e3d_dobs_ln1b>`
| **N_TRX** :math:`\;` :ref:`n_trx<e3d_dobs_ln1>`
|
|
| :ref:`DEFINE TRANSMITTER<e3d_dobs_transmitter>`
| 
| **FREQUENCY** :math:`\;` :ref:`f1<e3d_dobs_ln5>`
| **N_RECV** :math:`\;` :ref:`n_recv<e3d_dobs_ln6>`
| :math:`\;\;` :ref:`Data Array<e3d_dobs_ln7>`
|
|
| :ref:`DEFINE TRANSMITTER<e3d_dobs_transmitter>`
|
| **FREQUENCY** :math:`\;` :ref:`f2<e3d_dobs_ln5>`
| **N_RECV** :math:`\;` :ref:`n_recv<e3d_dobs_ln6>`
| :math:`\;\;` :ref:`Data Array<e3d_dobs_ln7>`
|
|
| :math:`\;\;\;\;\;\; \vdots`
|
|
| :ref:`DEFINE TRANSMITTER<e3d_dobs_transmitter>`
|
| **FREQUENCY** :math:`\;` :ref:`fn<e3d_dobs_ln5>`
| **N_RECV** :math:`\;` :ref:`n_recv<e3d_dobs_ln6>`
| :math:`\;\;` :ref:`Data Array<e3d_dobs_ln7>`
|
| *Repeat for number of unique transmitter-frequency pairs*
|
|



Parameter Descriptions
----------------------

.. _e3d_dobs_ln1b:

    - **reg_exp:** Regular expression (flag) used to data points that are ignored during the inversion

.. _e3d_dobs_ln1:

    - **n_trx:** The total number of transmitters. Example: *N_TRX 3*


.. _e3d_dobs_ln5:

    - **fi:** The frequency (in Hz) at which the subsequent set of measurements are made.

.. _e3d_dobs_ln6:

    - **n_recv:** The number of receivers collecting field observations at a particular frequency for a particular transmitter.

.. _e3d_dobs_ln7:

    - **Data Array:** Contains the X (Easting), Y (Northing) and Z (elevation) locations, observations and uncertainties at a particular frequency for a particular transmitter. It has dimensions :ref:`n_recv<e3d_dobs_ln6>` :math:`\times` 27.



.. _e3d_dobs_transmitter:

Defining Transmitters
---------------------

There are three types of transmitters that *E3D* survey files can use. These were defined in the :ref:`survey file section <e3d_survey_transmitter>`.



Data Array
----------

**E3DRH uses a right-handed Cartesian coordinate system. The vector components of the fields are therefore X: Easting direction, Y: Northing direction and Z: positive upward direction.** For each transmitter at each frequency, a set of field observations are made for a set of receivers. These field observations include real and imaginary components of the electric and magnetic fields as well as their uncertainties. The rows of the data array are formatted as follows:

.. math::
    | \; x \; | \; y \; | \; z \; | \;\;\; E_x \; data \;\;\; | \;\;\; E_y \; data \;\;\; | \;\;\; E_z \; data \;\;\; | \;\;\; H_x \; data \;\;\; | \;\;\; H_y \; data \;\;\; | \;\;\; H_z \; data \;\;\; |

such that :math:`E_x \; data` is comprised of 4 columns:

.. math::

    | \; E_x^\prime \; | \; U_x^\prime \; | \; E_x^{\prime \prime} \; | \; U_x^{\prime \prime} \; |

where

    - :math:`E_x^\prime` is the real component of the electric field along the Easting direction
    - :math:`E_x^{\prime\prime}` is the imaginary component of the electric field along the Easting direction
    - :math:`U_x^\prime` is the uncertainty on :math:`E_x^\prime`
    - :math:`U_x^{\prime\prime}` is the uncertainty on :math:`E_x^{\prime\prime}`


This is done likewise for :math:`E_y`, :math:`E_z`, :math:`H_x`, :math:`E_y`, :math:`H_z`.






