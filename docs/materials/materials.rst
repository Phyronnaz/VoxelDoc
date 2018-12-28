=========
Materials
=========

When using voxels, you usually want to be able to have any material on each voxel.
When using smooth voxels like marching cubes, you also want those materials to blend smoothly and not change abruptly.
In other words, you want to be able to blend any material with any other.

There are multiple use cases:

* Your materials are just colors, or you have a single material: see the :ref:`RGB-config` config
* Your materials have textures: see the :ref:`SingleIndex-config` and :ref:`DoubleIndex-config` configs

----------------
Material Configs
----------------

You can choose between the following configs using the **Material Config** property under the *Materials* category in the voxel world details.

.. _RGB-config:

^^^
RGB
^^^

In this mode, a single material is applied to all the voxels.
You can pass parameters to it through vertex colors using the voxel graph **Set Color** node or the C++ function **FVoxelMaterial::SetColor**.

You should choose this mode if your materials are only colors, or if you have a single material.

Voxel material usage:

* Red: Free
* Green: Free
* Blue: Free
* Alpha: Free

What is sent through vertex colors:

* Red: the voxel material Red component
* Green: the voxel material Green component
* Blue: the voxel material Blue component
* Alpha: the voxel material Alpha component

Pros:

* Low draw call count (one per chunk)
* Can have any color you want

Cons:

* Only one material, so won't work if you have more materials

.. _SingleIndex-config:

^^^^^^^^^^^^
Single Index
^^^^^^^^^^^^

This mode uses :ref:`material-collections`.

You set a material index to every voxel using the voxel graph node **Set Index** or the C++ function **FVoxelMaterial::SetIndex**,
and the plugin will set to that voxel the matching material collection material.
If different materials are next to each others, it'll blend them accordingly.

Voxel material usage:

* Red: Free
* Green: Free
* Blue: Free
* Alpha: to store the index

What is sent through vertex colors:

* Red: blend parameter
* Green: blend parameter
* Blue: the voxel material Blue component
* Alpha: the voxel material Alpha component, here the index

Pros:

* Very easy to use, no need to worry about the blending
* Can use all the materials you want at a constant cost

Cons:

* Can lead to imperfect blending between different materials.
  Indeed, the blending is based on the triangles: the correct material will be chosen based on the vertices material indices.
  If you have a very small triangle, the blending might be only in it and thus invisible.
* Higher draw call count than the RGB config as it needs to create new meshes for each material.

.. _DoubleIndex-config:

^^^^^^^^^^^^
Double Index
^^^^^^^^^^^^

This mode also uses :ref:`material-collections`.

You set on each voxels 3 values:

* a material index A
* a material index B
* a lerp parameter alpha

using the voxel graph node **Set Double Index** or the C++ functions **FVoxelMaterial::SetIndexA/SetIndexB/SetBlend**.

The displayed material will be Lerp(A, B, alpha). If alpha is 0 or 1, the plugin will optimize and use a single material instead of a double material.

Voxel material usage:

* Red: to store the index A
* Green: to store the index B
* Blue: to store the alpha
* Alpha: Free

What is sent through vertex colors:

* Red: blend parameter
* Green: the voxel material Green component, here the index B
* Blue: the voxel material Blue component, here the alpha
* Alpha: the voxel material Alpha component

Pros:

* Much more control on the blending
* Can use all the materials you want at a constant cost

Cons:

* Need some thinking to set the parameters correctly if you want smooth blending
* Higher draw call count than the RGB config as it needs to create new meshes for each material.

--
UV
--

There are four UV modes:

* **Global UVs**: U = Global Position X and V = Global Position Y.
  Useful to quickly test materials without adding some triplanar projection to them, but has issues if your voxels aren't all more or less facing up.

* **Use Red and Green as UVs**: U = voxel material R component and V = voxel material G component.
  Useful if you want to pass additional parameters to your material when using the Single Index/Double Index configs.

* **Pack WorldUp in UVs**: pack the world generator up vector in the UVs.
  You can recover it like that:
    
    * X = U
    * Y = V
    * Z = sqrt(1 - U\*U - V\*V)

* **Per Voxel UVs**: for the cubic mode only. The UVs will be set to a basic cube UVs for each voxel.

.. important::

    If you're using the marching cube mode, you should use triplanar projection in your materials.
    There are plenty of tutorials on the internet on how to do this.

------
Normal
------

There are three normal modes:

* **No Normal**: no normal are computed except on the chunk borders where they are needed for the transvoxel transitions.

* **Gradient Normal**: use the density field gradient to compute the normal.
  If it doesn't look good, try to divide the output value your world generator by eg 10:
  as the voxel values are clamped between -1 and 1, this allows you to gain some precision that would be lost by the clamping.

* **Mesh Normal**: compute the normal from the triangles,
  unless on the chunk borders where gradient normal are used because mesh normal aren't the same for different chunks.

------------
Tessellation
------------

To enable tessellation, tick the **Tessellation** property under the *Materials* category in the voxel world details.

Unlike UE landscapes, tessellation isn't enabled on the whole world: indeed, even with a tessellation multiplier of 0,
it still adds a considerable cost due to the tessellation shader still being ran.
To improve that, tessellation is only enabled on close chunks.
This can be controlled by the **Tessellation Max LOD** property:

* On chunks with a LOD inferior or equal to it, a tessellated material is used:

    * **VoxelWorld Material with Tessellation** if material config = RGB
    * The tessellated materials generated by the material collection else (you need to have **Enable Tessellation** ticked in it)

* On other chunks, the normal materials without tessellation are used

While this is meant for tessellation switch, you can also use it to disable some material features on far chunks.
To switch in the material collection you can use the **IsTessellationEnabled** static switch.
