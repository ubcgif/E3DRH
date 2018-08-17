.. _indexFile:

Survey Index File
=================

This file is input when forward modeling data. Using 4 columns, the observation file indexes the frequencies, transmitters and receivers used for each measurement. Each row defines a unique field measurement. The general format is as follows:


| :ref:`tx_ind<aem_survey_ln1>` :math:`\;` :ref:`f_ind<aem_survey_ln2>` :math:`\;` :ref:`rx_ind<aem_survey_ln3>` :math:`\;` :ref:`data_opt<aem_survey_ln4>`
| :ref:`tx_ind<aem_survey_ln1>` :math:`\;` :ref:`f_ind<aem_survey_ln2>` :math:`\;` :ref:`rx_ind<aem_survey_ln3>` :math:`\;` :ref:`data_opt<aem_survey_ln4>`
| :ref:`tx_ind<aem_survey_ln1>` :math:`\;` :ref:`f_ind<aem_survey_ln2>` :math:`\;` :ref:`rx_ind<aem_survey_ln3>` :math:`\;` :ref:`data_opt<aem_survey_ln4>`
| :math:`\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\; \vdots`
| :ref:`tx_ind<aem_survey_ln1>` :math:`\;` :ref:`f_ind<aem_survey_ln2>` :math:`\;` :ref:`rx_ind<aem_survey_ln3>` :math:`\;` :ref:`data_opt<aem_survey_ln4>`
|
|


.. important:: 
    Due to the way the forward problem is solved, it is imperative that the user sort the survey index file:
        - First by transmitter
        - Next by frequency
        - Then finally by receiver


**Parameter Descriptions**


.. _aem_survey_ln1:

    - **tx_ind:** The index corresponding to the desired transmitter within the :ref:`transmitter file<receiverFile>`. 

.. _aem_survey_ln2:

    - **f_ind:** The index corresponding to the desired frequency within the :ref:`frequencies file<freqFile>`.

.. _aem_survey_ln3:

    - **rx_ind:** The index corresponding to the desired receiver within the :ref:`receiver file<receiverFile>`.

.. _aem_survey_ln4:

    - **1:** As of May 2018, a flag value of 1 is entered here. In future iterations of the code, this entry may be related to additional functionality.




