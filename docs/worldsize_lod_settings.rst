=========================
World Size & LOD settings
=========================

----------
World Size
----------

The following properties can be used in the voxel world details *World Size* category to control the world size:

* **Octree Depth**: the depth of the octree of the voxel world
* **World Size**: the size of the world, given by the octree depth: *CHUNK_SIZE * 2^octree_depth*

However, these settings aren't really precise.
For a more precise control the **Override Bounds** and **World Bounds** properties can be used.

.. warning::

    Chunks with a high LOD might ignore the custom bounds.
    To fix this, you can add a check in your world generator to return 1 when the position is outside the bounds.

.. tip::

    You can debug the world bounds by using the **Show World Bounds** and **World Bounds Thickness**
    properties in the *Voxel/Debug* category of the voxel world details,
    or by using the **voxel.ShowWorldBounds** command

^^^^^^^^^^^^^^^^^^^^^^^^^^
Performance considerations
^^^^^^^^^^^^^^^^^^^^^^^^^^

You should use bounds as small as possible to improve the generation speed.

If for instance you have a world size of 4096, 4096 x 4096 x 4096 voxels will be generated.
However if your world doesn't go deeper than -256 voxels and higher than 512,
not all those voxels are needed: using custom bounds like **(-2048, -2048, -256), (2048, 2048, 512)**
will improve performance a lot for the same visual results.

------------
LOD Settings
------------

The LODs are determined by the **Voxel Invokers Components** in the scene.
Usually you only need a single voxel invoker on your character.

The following properties can be used in the voxel world details *LOD Settings* category to control the LODs:

* **LOD Limit**: the chunks can't have a LOD higher than this.
  Useful if you don't want to have a very low poly look when you're far from your world.
  If you don't want any LOD, you can set it to 0.

* **LOD to Min Distance**: If LODToMinDistance[L] = D, then all the chunks under a distance D from a voxel invoker
  (in world space) will have a LOD inferior or equal to L.

.. warning::

    Be careful when changing the LOD settings, as you can easily freeze UE & use all the available RAM
    with too high settings (eg LOD Limit of 0 on a big world).

.. tip:: text
    attention, caution, danger, error, hint, important, note, tip, warning