.. _preFile:

Predicted Data File
===================

E3D version 2 models magnetic field data in a **left-handed** coordinate system where X is Easting, Y is Northing and Z is +ve downwards. For a given model, E3D version 2 computes the data by integrating the electric field (:math:`\mathbf{E}`) over each receiver loop to obtain the induced EMF, then uses the dipole moment of the receiver and Faraday's law to represent the voltage in the coil as magnetic field value:

.. math::
	H = \frac{1}{i\omega \mu A} \, \oint_C \mathbf{E} \cdot d \mathbf{l}

If the receive loop is sufficiently small, the data are just the dot product of the total field :math:`\mathbf{H}` with the direction defining the receiver's dipole moment:

.. math::
	H = \mathbf{H} \cdot \frac{\mathbf{m}}{| \mathbf{m} |}


Predicted data files output from **e3dinv_ver2.exe** have a simple 2 column format. Column 1 contains the real component of the total magnetic field data measured by the receiver, and column 2 contains the imaginary component. The rows are ordered the same as in the :ref:`survey index<indexFile>` or :ref:`observations<obsFile>` file. Thus predicted data files take the format:

|
| :math:`H_1^\prime \;\; H_1^{\prime\prime}`
| :math:`H_2^\prime \;\; H_2^{\prime\prime}`
| :math:`H_3^\prime \;\; H_3^{\prime\prime}`
|
| :math:`\;\;\;\;\;\;\;\; \vdots`
|
| :math:`H_4^\prime \;\; H_4^{\prime\prime}`
|
|















