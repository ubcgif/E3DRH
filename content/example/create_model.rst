.. _example_model:

Create Model
============

Here, the code **blk3cellOct.exe** and the input file **blk3cellOct.inp** (:ref:`see format <e3d_input_model>`) are used to create a conductivity model on the OcTree mesh. For this example, we use the mesh that was created in the example ":ref:`create OcTree mesh<example_octree>`". Files relevant to this part of the example are in the sub-folder *octree_model*. Before running this example, you may want to do the following:

	- `Download and open the zip folder containing the entire E3DRH version 1 example <https://github.com/ubcgif/E3DRH/raw/e3drh/assets/e3drh_example.zip>`__ (if not done already)
	- Learn how to run :ref:`blk3cellOct<e3d_model>`
	- Learn the format of the input files :ref:`blk3cellOct.inp<e3d_input_model>`


Here is the input file for **blk3cellOct.exe**

.. figure:: ../inputfiles/images/create_blk3cellOct_input.png
     :align: center
     :width: 700


The resulting Octree model shows a more conductive block (:math:`\sigma` = 0.01 S/m) within a more resistive background (:math:`\sigma_b` = 0.0001 S/m). A constant topography of 0 m in elevation is shown in gray. The observation locations are shown in blue.


.. figure:: images/octree_model1.png
     :align: center
     :width: 500


