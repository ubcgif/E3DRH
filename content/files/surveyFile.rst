.. _surveyFile:

Survey and Locations File
=========================

The survey and locations file is used to predict synthetic field data (forward modeling). This file contains all necessary survey information including: the number of transmitters, transmitter geometry, observation locations and frequencies. 

.. note:: Bolded entries are fixed flags recognized by the Fortran codes and blue hyperlinked entries are values/regular expressions specified by the user


The lines of the survey file are formatted as follows:

|
| **N_TRX** :math:`\;` :ref:`n_trx<e3d_survey_ln1>`
|
|
| :ref:`DEFINE TRANSMITTER<e3d_survey_transmitter>`
| 
| **FREQUENCY** :math:`\;` :ref:`f1<e3d_survey_ln5>`
| **N_RECV** :math:`\;` :ref:`n_recv<e3d_survey_ln6>`
| :math:`\;\;` :ref:`Loc Array<e3d_survey_ln7>`
|
|
| :ref:`DEFINE TRANSMITTER<e3d_survey_transmitter>`
|
| **FREQUENCY** :math:`\;` :ref:`f2<e3d_survey_ln5>`
| **N_RECV** :math:`\;` :ref:`n_recv<e3d_survey_ln6>`
| :math:`\;\;` :ref:`Loc Array<e3d_survey_ln7>`
|
|
| :math:`\;\;\;\;\;\; \vdots`
|
|
| :ref:`DEFINE TRANSMITTER<e3d_survey_transmitter>`
|
| **FREQUENCY** :math:`\;` :ref:`fn<e3d_survey_ln5>`
| **N_RECV** :math:`\;` :ref:`n_recv<e3d_survey_ln6>`
| :math:`\;\;` :ref:`Loc Array<e3d_survey_ln7>`
|
| *Repeat for number of unique transmitters*
|
|


.. figure:: images/files_locations.png
     :align: center
     :width: 400

     Example survey file with various types of transmitters.



Parameter Descriptions
----------------------


.. _e3d_survey_ln1:

    - **n_trx:** The total number of unique transmitter-frequency pairs. Example: *N_TRX 3*

.. _e3d_survey_ln3:

    - **n_nodes:** The number of nodes defining a particular transmitter loop. Note that:

.. _e3d_survey_ln4:

    - **xi yi zi:** This refers to the X (Easting), Y (Northing) and Z (elevation) locations of the nodes defining the transmitter loop. Transmitters are defined using a left-handed coordinate system. Which means you must define a horizontal transmitter loop in the clockwise direction for a dipole moment in the vertical direction.

.. _e3d_survey_ln5:

    - **fi:** The frequency (in Hz) at which the subsequent set of measurements are made.

.. _e3d_survey_ln6:

    - **n_recv:** The number of receivers collecting field observations at a particular frequency for a particular transmitter.

.. _e3d_survey_ln7:

    - **Loc Array:** Contains the X (Easting), Y (Northing) and Z (elevation) locations for measurements at a particular frequency for a particular transmitter. It has dimensions :ref:`n_recv<e3d_survey_ln6>` :math:`\times` 3.


.. _e3d_survey_transmitter:

Defining Transmitters
---------------------

There are three types of transmitters that *E3D* survey files can use

Circular loop transmitter
~~~~~~~~~~~~~~~~~~~~~~~~~

This is an inductive source. The circular loop transmitter is defined using two lines:

|
| *TRX_LOOP*
| :math:`x \;\; y \;\; z \;\; R \;\; \theta \;\; \alpha`
|
|

where

    - *TRX_LOOP* is a flag that must be entered
    - :math:`x` is the Easting, :math:`y` is the Northing and :math:`z` is the elevation location of the center of the loop
    - :math:`R` is the radius of the loop
    - :math:`\theta` is the azimuthal angle in degrees. A horizontal loop is defined by :math:`\theta = 0`
    - :math:`\alpha` is the clockwise angle from northing in degrees


Large inductive source
~~~~~~~~~~~~~~~~~~~~~~

Here, we define the inductive source using a set of wire segments. When defining this type of transmitter, you **must** close the loop. The block defining this transmitter is given by:

|
| *TRX_ORIG*
| :math:`N`
| :math:`x_1 \;\; y_1 \;\; z_1`
| :math:`x_2 \;\; y_2 \;\; z_2`
| :math:`\;\;\;\; \vdots`
| :math:`x_{N-1} \; y_{N-1} \;\; z_{N_1}`
| :math:`x_1 \;\; y_1 \;\; z_1`
| 
|

where

    - *TRX_ORIG* is a flag that must be entered
    - :math:`N` is the number of nodes (# segments - 1)
    - :math:`x_i, \; y_i \; z_i` are Easting, Northing and elevation locations for the nodes



Arbitrary source
~~~~~~~~~~~~~~~~

Using this transmitter type, we can define both inductive sources (by closing the loop) or grounded sources (by not closing the loop). The block defining this transmitter is given by:

|
| *TRX_LINES*
| :math:`N`
| :math:`x_1 \;\; y_1 \;\; z_1`
| :math:`x_2 \;\; y_2 \;\; z_2`
| :math:`\;\;\;\; \vdots`
| :math:`x_{N} \; y_{N} \;\; z_{N}`
| 
|

where

    - *TRX_LINES* is a flag that must be entered
    - :math:`N` is the number of nodes (# segments - 1)
    - :math:`x_i, \; y_i \; z_i` are Easting, Northing and elevation locations for the nodes

















