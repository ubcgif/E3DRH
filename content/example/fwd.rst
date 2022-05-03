.. _example_fwd:

Forward Modeling
================

Here, the code **e3drh_v2_tiled.exe** and the input file **e3dfwd.inp** (:ref:`see format <e3d_input_fwd>`) are used to forward model secondary field FEM data for a synthetic airborne survey. The transmitter loop is horizontal and flown 75 m above the surface. The receiver is located 125 m above the surface (so there is a vertical offset between the transmitter and receivers) and measures the vertical component of the magnetic field. Files relevant to this part of the example are in the sub-folder *fwd*. For this example, we use the model that was created in the example ":ref:`create model<example_model>`". Before running this example, you may want to do the following:


	- `Download and open the zip folder containing the entire E3DRH version 2 tiled example <https://github.com/ubcgif/E3DRH/raw/e3drh_v2_tiled/assets/e3drh_v2_tiled_example.zip>`__ (if not done already)
	- :ref:`Learn how to run code from command line <e3d_fwd>`
	- :ref:`Learn the format of the input file <e3d_input_fwd>`

To forward model the data, the following input file was used:

.. figure:: ../inputfiles/images/create_fwd_input.png
     :align: center
     :width: 700


Below we show the real and imaginary components of the vertical secondary magnetic field at 2500, 10,000 and 40,000 Hz. We defined the transmitter loop using the right-hand rule so that the primary magnetic field at the center of the loop would be pointing upward (+ve Hz). Since we are using an :math:`e^{-i\omega t}` Fourier convention Fourier convention, the right-hand rule was used to define a receiver loop that would meause the component of the magnetic in the upward direction (+ve z). Notice that the real component of Hz-secondary is -ve; i.e. the secondary field opposes the primary field. Notice also that the real and imaginary components of the secondary field are opposite. This also occurs because the forward problem is solved using an :math:`e^{-i\omega t}` Fourier convention.

.. figure:: images/fwd_tiled.png
     :align: center
     :width: 700



