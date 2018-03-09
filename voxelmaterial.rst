Voxel Material
==============

A *Voxel Material* has 4 properties:

* 2 materials index (A and B)
* an alpha
* a Voxel Actor ID

The final material is Lerp(A, B, alpha). The Voxel Actor ID is used for Voxel Actors spawn.

This means you can't have more than 2 materials on a single voxel: this is problematic when painting for instance.

This is also why Voxel Tools that paint the world have a Layer parameter: Layer = 0 means the index A is changed, and Layer = 1 means it's the B that's modified.

This also lead to issues similar to those below:

.. image:: img/voxelmaterial_glitches.png