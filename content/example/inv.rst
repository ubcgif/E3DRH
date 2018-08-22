.. _example_inv:

Inversion
=========

Here, the code **e3dinv_ver2.exe** and the input file **e3dinv_ver2.inp** (:ref:`see format <e3d_input_inv>`) are used to invert Hz data. FEM data were created in the example ":ref:`forward modeling<example_fwd>`". Uncertainties of 1e-7 V/m :math:`\pm` 5\% were used. Basic uncertainties were added for the sake of keeping the example simple. In practice, data are noisy and choosing appropriate uncertainties is very important for successful inversion. Files relevant to this part of the example are in the sub-folder *inv*. Before running this example, you may want to do the following:

	- `Download and open the zip folder containing the entire E3D version 2 example <https://github.com/ubcgif/E3D/raw/e3dinv_ver2/assets/e3d_ver2_example.zip>`__ (if not done already)
	- :ref:`Learn how to run code from command line <e3d_inv>`
	- :ref:`Learn the format of the input file <e3d_input_inv>`

To invert the synthetic data, the input file below was used:

.. figure:: ../inputfiles/images/create_inv_input.png
     :align: center
     :width: 700


The true model (left) and recovered model (right) at iteration 5 are shown below. A cutoff of 0.05 S/m has been used for both models and the recovered model is transected at z = -1200 m. 

.. figure:: images/inv1.png
     :align: center
     :width: 700

