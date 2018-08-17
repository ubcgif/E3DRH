.. _binaryFile:

Local Meshes in binary File
================================

The local Octree meshes used to solve forward problems parallel are stored in a binary file. The ordering of local OcTree meshes in this file is the same as the ordering of transmitter indexes in the :ref:`survey index<indexFile>` or :ref:`observations<obsFile>` that was used to make the meshes. The user may extract any local mesh and save it as a :ref:`standard OcTree mesh<octreeFile>` by running the :ref:`extract_mesh<>` code.



