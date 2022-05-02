.. _example:

.. important:: In the spring of 2022, a new suite of FDEM OcTree codes were compiled: *E3DRH, E3DRH v2 and E3DRH v2 tiled*. **These codes use a right-handed coordinate system**; as opposed to the modified left-handed coordinate system used by *E3D, E3D v2 and E3D v2 tiled*. **You are currently viewing the manual for the package which uses 'e3drh_v2_tiled.exe' to forward model and invert FDEM data**. The manual for the original E3D v2 tiled package (which uses 'e3d_v2_tiled.exe') `can be found here <https://e3d.readthedocs.io/en/e3d_v2_tiled/>`__ .

Examples
========

Here, the program library for E3DRH version 2 tiled will be used to:

	- create an Octree mesh based on the survey
	- create octree models
	- predict frequency-domain airborne data for a synthetic model
	- invert the data to recover our synthetic model

Zip folders containing all necessary files can be downloaded here:

	- `Files for example using E3DRH version 2 tiled <https://github.com/ubcgif/e3d/raw/e3drh_v2_tiled/assets/e3drh_v2_tiled_example.zip>`__

The full examples are parse into 4 sections:

.. toctree::
    :maxdepth: 2

    Create octree mesh <example/create_octree>
    Create octree model <example/create_model>
    Forward modeling <example/fwd>
    Inversion <example/inv>

