.. _obsFile:

Observations File
=================

This file is input when forward modeling or inverting field-collected data. Using 8 columns, the observation file indexes the frequencies, transmitters and receivers used for each measurement as well as the field observations and data uncertainties. Each row defines a unique field measurement. The general format is as follows:

.. note::
    - Blue hyperlinked entries are values specified by the user
    - To omit a particular datum in the inversion, used the flag **-99** on its corresponding uncertainty.



| :ref:`tx_ind<aem_obs_ln1>` :math:`\;` :ref:`f_ind<aem_obs_ln2>` :math:`\;` :ref:`rx_ind<aem_obs_ln3>` :math:`\;` :ref:`data_opt<aem_obs_ln4>` :math:`\;` :ref:`data_real<aem_obs_ln5>` :math:`\;` :ref:`unc_real<aem_obs_ln6>` :math:`\;` :ref:`data_imag<aem_obs_ln7>` :math:`\;` :ref:`unc_imag<aem_obs_ln8>`
| :ref:`tx_ind<aem_obs_ln1>` :math:`\;` :ref:`f_ind<aem_obs_ln2>` :math:`\;` :ref:`rx_ind<aem_obs_ln3>` :math:`\;` :ref:`data_opt<aem_obs_ln4>` :math:`\;` :ref:`data_real<aem_obs_ln5>` :math:`\;` :ref:`unc_real<aem_obs_ln6>` :math:`\;` :ref:`data_imag<aem_obs_ln7>` :math:`\;` :ref:`unc_imag<aem_obs_ln8>`
| :ref:`tx_ind<aem_obs_ln1>` :math:`\;` :ref:`f_ind<aem_obs_ln2>` :math:`\;` :ref:`rx_ind<aem_obs_ln3>` :math:`\;` :ref:`data_opt<aem_obs_ln4>` :math:`\;` :ref:`data_real<aem_obs_ln5>` :math:`\;` :ref:`unc_real<aem_obs_ln6>` :math:`\;` :ref:`data_imag<aem_obs_ln7>` :math:`\;` :ref:`unc_imag<aem_obs_ln8>`
| :math:`\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\; \vdots`
| :ref:`tx_ind<aem_obs_ln1>` :math:`\;` :ref:`f_ind<aem_obs_ln2>` :math:`\;` :ref:`rx_ind<aem_obs_ln3>` :math:`\;` :ref:`data_opt<aem_obs_ln4>` :math:`\;` :ref:`data_real<aem_obs_ln5>` :math:`\;` :ref:`unc_real<aem_obs_ln6>` :math:`\;` :ref:`data_imag<aem_obs_ln7>` :math:`\;` :ref:`unc_imag<aem_obs_ln8>`
|
|

.. important:: 
    Due to the way the forward problem is solved, it is imperative that the user sort the observations:
        - First by transmitter
        - Next by frequency
        - Then finally by receiver


**Parameter Descriptions**


.. _aem_obs_ln1:

    - **tx_ind:** The index corresponding to the desired transmitter within the :ref:`transmitter file<receiverFile>`. 

.. _aem_obs_ln2:

    - **f_ind:** The index corresponding to the desired frequency within the :ref:`frequencies file<freqFile>`.

.. _aem_obs_ln3:

    - **rx_ind:** The index corresponding to the desired receiver within the :ref:`receiver file<receiverFile>`.

.. _aem_obs_ln4:

    - **1:** As of May 2018, a flag value of 1 is entered here. In future iterations of the code, this entry may be related to additional functionality.

.. _aem_obs_ln5:

    - **data_real:** The real component of the observed data.

.. _aem_obs_ln6:

    - **unc_real:** The uncertainty for the real component of the observed data.

.. _aem_obs_ln7:

    - **data_imag:** The imaginary component of the observed data.

.. _aem_obs_ln8:

    - **unc_imag:** The uncertainty for the real component of the observed data.












