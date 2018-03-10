General Concept
===============

Plugin structure overview:

.. image:: img/VoxelMain.svg

To render the world, the plugin uses the **Marching Cubes** algorithm.
You can read a quick introduction to this algorithm here_.

.. _here: http://paulbourke.net/geometry/polygonise/

The marching cubes algorithm requires a density field.


Density field
-------------

* A density is a float between -1 and 1, 1 being empty and -1 full. 
* The sign of the density determines its side: negative = inside, positive = outside.
* The absolute value of the density determines its distance to the surface, 0 being on the surface.
* A density field is a 3D space where the density is known at every integer position.

Local space vs Global space
---------------------------

The Voxel World uses 2 coordinate systems: 

* a local one, used for the voxels. The positions are **FIntVectors**.
* the global one is the UE coordinate systems

To switch between those coordinate systems, you can use the :ref:`GlobalToLocal` and :ref:`LocalToGlobal` functions.