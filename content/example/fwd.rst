.. _example_fwd:

Forward Modeling
================

Here, the code **e3drh.exe** and the input file **e3dfwd.inp** (:ref:`see format <e3d_input_fwd>`) are used to forward model secondary field FEM data for a synthetic airborne survey. The transmitter loop is horizontal and flown 75 m above the surface. The receiver is located 125 m above the surface (so there is a vertical offset between the transmitter and receivers). Files relevant to this part of the example are in the sub-folder *fwd*. For this example, we use the model that was created in the example ":ref:`create model<example_model>`". Before running this example, you may want to do the following:

	- `Download and open the zip folder containing the entire E3DRH version 1 example <https://github.com/ubcgif/E3DRH/raw/e3drh/assets/e3drh_example.zip>`__ (if not done already)
	- :ref:`Learn how to run code from command line <e3d_fwd>`
	- :ref:`Learn the format of the input file <e3d_input_fwd>`

To forward model the data, the following input file was used:

.. figure:: ../inputfiles/images/create_fwd_input.png
     :align: center
     :width: 700

We used E3D version 1 to forward model the Cartesian components of the electric field and secondary magnetic field. Below we show the real and imaginary components of the vertical secondary magnetic field at 2500, 10,000 and 40,000 Hz. We defined the transmitter loop using the right-hand rule so that the primary magnetic field at the center of the loop would be pointing upward (+ve Hz). Notice that the real component of Hz-secondary is -ve; i.e. the secondary field opposes the primary field. Notice also that the real and imaginary components of the secondary field are opposite. This occurs because the forward problem is solved using an :math:`e^{-i\omega t}` Fourier convention.

.. figure:: images/fwd1.png
     :align: center
     :width: 700



