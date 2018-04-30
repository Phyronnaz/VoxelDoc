Voxel Material
==============

A *Voxel Material* has 4 properties:

* 2 materials index (A and B)
* an alpha
* a Voxel Actor ID

The final material is Lerp(A, B, alpha). The Voxel Actor ID is used for Voxel Actors spawn.

The Voxel Material is passed to the UE Material through Vertex Colors:

* R -> A
* G -> B
* B -> Alpha
* A -> Unused

A custom vertex factory disable interpolation on R and G.

Limit
------

This means you can't have more than 2 materials on a single voxel: this is problematic when painting for instance.

This is also why Voxel Tools used to paint the world have a Layer parameter: Layer = 1 means the index A is changed, and Layer = 2 means it's the B that's modified.

This also lead to issues similar to those below:

.. image:: img/voxelmaterial_glitches.png

Workaround
----------

This limit is due to using only 2 layers. If you need more, or if you have a different idea on how to handle materials, create an issue on Github or leave a message on the Discord.

To avoid glitches, you must always make sure you're painting on a different layer: layer 1 on layer 2, or layer 2 on layer 1.