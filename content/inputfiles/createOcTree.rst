.. _e3dmt_input_octree:

Create OcTree Mesh Input File
=============================

The :ref:`OcTree mesh<octreeFile>` used in the E3D code are created using the program **create_octree_mesh_e3d.exe**. Parameters necessary for defining the OcTree mesh are set in the input file. The lines within the input file are as follows:


.. tabularcolumns:: |C|C|C|

+--------+----------------------------------------------------------+-----------------------------------------------------------------+
| Line # | Parameter                                                | Descriptions                                                    |
+========+==========================================================+=================================================================+
| 1      |:ref:`dx dy dz<e3dmt_input_octreeln1>`                    | min. cell widths in x, y and z for base mesh                    |
+--------+----------------------------------------------------------+-----------------------------------------------------------------+
| 2      |:ref:`x_pad y_pad down_pad up_pad<e3dmt_input_octreeln2>` | sets the extend of mesh in x, y and z direction                 |
+--------+----------------------------------------------------------+-----------------------------------------------------------------+
| 3      |:ref:`dist_1 dist_2 dist_3<e3dmt_input_octreeln3>`        | sets cell sizes within core mesh region                         |
+--------+----------------------------------------------------------+-----------------------------------------------------------------+
| 4      |:ref:`n1 n2 n3<e3dmt_input_octreeln4>`                    | sets thickness of cells of finest discretization near receivers |
+--------+----------------------------------------------------------+-----------------------------------------------------------------+
| 5      |:ref:`locFile<e3dmt_input_octreeln5>`                     | the file containing transmitters and observation locations      |
+--------+----------------------------------------------------------+-----------------------------------------------------------------+
| 6      |:ref:`topoFile<e3dmt_input_octreeln6>`                    | sets topography                                                 |
+--------+----------------------------------------------------------+-----------------------------------------------------------------+
| 7      |:ref:`shift_data<e3dmt_input_octreeln7>`                  | *description needed. leave as NOT_SHIFT_DATA*                   |
+--------+----------------------------------------------------------+-----------------------------------------------------------------+
| 8      |:ref:`interp_topo<e3dmt_input_octreeln8>`                 | sets level of discretization for surface topography             |
+--------+----------------------------------------------------------+-----------------------------------------------------------------+


.. | 9      |:ref:`start_point<e3dmt_input_octreeln9>`                 | sets the starting point for the mesh generation                 |
.. +--------+----------------------------------------------------------+-----------------------------------------------------------------+


.. figure:: images/create_octree_input.png
     :align: center
     :width: 700

     Example input file for creating octree mesh (`Download <https://github.com/ubcgif/e3dmt/raw/master/assets/input_files1/MTcreate_mesh.inp>`__ )


Line Descriptions
^^^^^^^^^^^^^^^^^


.. _e3dmt_input_octreeln1:

    - **dx dy dz:** Minimum cell widths in x, y and z for the base mesh.

.. _e3dmt_input_octreeln2:

    - **x_pad y_pad down_pad up_pad:** Distance from the origin in the x, y, downward and upward directions, respectively, that the mesh extends.

.. _e3dmt_input_octreeln3:

    - **dist_1 dist_2 dist_3:** Sets the distance from surface topography and receivers in which the cells widths are increased by a factor of 2 in x, y and z. Up to a depth of *dist_1* from surface topography and within a horizontal distance of *dist_1* from any receiver, the smallest cell size is used (set by *dx, dy, dz*). For the following *dist_2* metres, the cell widths are doubled. For the following *dist_3* metres, the cell widths are doubled again. Outside a depth and horizontal distance of *h1+h2+h3*, the cells widths increase by a factor of 2 for every additional layer (see the figure below).

.. _e3dmt_input_octreeln4:

    - **n1 n2 n3:** This sets the thicknesses of layers of finest discretization near the receivers. **n1 = 4** means that around each receiver, there is a layer 4 cells thick that uses the finest discretization. This is followed by a layer which is **n2** cells thick, where the cell dimensions are increased by a factor of 2. Likewise for the 3rd layer.

.. _e3dmt_input_octreeln5:

    - **locFile:** Contains the locations of the receivers. The user may either enter the file path to an :ref:`observed data<obsFile>` file, or the flag "ONLY_LOC" followed by the path to a :ref:`data points<surveyFile>` file. 

.. _e3dmt_input_octreeln6:

    - **topoFile:** If a topography file is available, the file path to the topography file is entered; see :ref:`topography file<topoFile>` for format. In the case of flat topography, the user instead enter "TOPO_CONST", followed by a space, then the elevation of the surface topography; for example "TOPO_CONST 125.5".

.. _e3dmt_input_octreeln7:

    - **shift_data:** Set as either "NOT_SHIFT_DATA" or "SHIFT_DATA *filename*". **EXPLANATION REQUIRED**

.. _e3dmt_input_octreeln8:

    - **interp_topo:** Set as either "APPROXTOPO" or "GOODTOPO". If "APPROXTOPO" is chosen, there will only be fine cells close to the survey, whereas "GOODTOPO" will place fine cells everywhere on the surface.

.. .. _e3dmt_input_octreeln9:

..     - **start_point:** Set as either "START_LARGE_CELLS" or "START_SMALL_CELLS". This line sets the starting point for the mesh generation. Starting the mesh population from large cells greatly reduces initial memory required and is therefore suggested. Large cells are divided in this algorithm to produce the OcTree mesh.


.. .. figure:: images/octree_example.png
..      :align: center
..      :width: 400

..      Octree mesh showing and surface topography. Cells below the surface topography are assigned a value of 1 in the active cells model.

Approximate versus Good Topography
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Below, we see the difference between entering "APPROXTOPO" (top) and "GOODTOPO" (bottom) into :ref:`interp_top<e3dmt_input_octreeln7>`. For "APPROXTOPO", the mesh ultimately contains a smaller total number of cells, as discretization near the surface is coarser. For "GOODTOPO", the mesh contains a larger total number of cells because the surface topography is discretized to the finest cell size.


.. figure:: images/create_octree_topo.png
     :align: center
     :width: 500









