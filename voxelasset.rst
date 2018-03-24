Voxel Asset
===========

.. raw:: html

    <div class="video-container"><iframe src="https://www.youtube.com/embed/-vU0z-rXySE?rel=0" frameborder="0" allowfullscreen></iframe></div>
    
.. raw:: html

	<p></p>

A *Voxel Asset* is a World Generator with bounds. This means you can use a voxel asset as world generator.
A Voxel Asset is created when you use an importer, but you can also create one yourself.

Creating a Voxel Asset from a World Generator
---------------------------------------------

* Right click in your Content Browser and create a new **Voxel Asset Builder**, and open It
* Set the world generator (for instance to **FlatWorldGenerator**)
* Set the bounds
* Set the **Offset**. This is useful to modify the asset origin: for instance if the bounds are (100, 100, 100) and (200, 200, 200), setting the offset to (-150, -150, -150) will recenter the asset.

Using Voxel Assets
------------------

You can use a Voxel Asset as a world generator. However, you can also import it at runtime into your world. There are 2 ways to do that:

Import Asset
~~~~~~~~~~~~

This is for small assets. It copies the asset data to the world. Call is expensive, but no impact on performance after.

Add Asset
~~~~~~~~~

This is for big assets (no limit in size). Instead of copying the data, it tells the Voxel World that there's an asset at the given position. Call is cheap, but impact the performance after. Don't use too many times on a same voxel world.

Voxel Assets created by importers
---------------------------------

Voxel Data Asset
~~~~~~~~~~~~~~~~

This asset is defined by a 3D array of values/materials/voxel types. Used for meshs, splines, 3D Coat, MagicaVox. Memory expensive.

Voxel Landscape Asset
~~~~~~~~~~~~~~~~~~~~~

This asset is defined by a 2D array of values/materials. It's relatively memory efficient.