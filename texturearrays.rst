Texture Arrays
==============

* Download the Texture Array engine build and plugin build. // TODO
* If you already have a Voxel World, remove it.
* Add a **VoxelWorld_TextureArrays** to your scene (Voxel Content/TextureArrays)
* Set the **Path**, **Diffuse Suffix** and **Normal Suffix** parameters. The blueprint will look recursively under *Path* for textures ending by *Diffuse Suffix*. For each texture found, it'll check if there's a texture with the same prefix ending by *Normal Suffix*. **WARNING:** All textures in the same array (diffuse array or normal array) must have the same resolution and the same pixel format. Check the output log for errors. To change a texture resolution, you can use **LOD Bias**:

.. image:: img/texturearrays_lodbias.png

* Hit play. If you have a lot of textures, the loading can be a bit long.
* Check the output log for errors.
* The textures should appear in the UI:

.. image:: img/texturearrays_result.png