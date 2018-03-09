Voxel Type
==========

A *Voxel Type* is used when merging world generators, and more particulary voxel assets.

It has 2 properties:

VoxelValueType
--------------

3 possible values:

* IgnoreValue: Value shouldn't be used
* UseValueIfSameSign: use the value if the 2 worlds are empty at this position, or if they are both full
* UseValue: the value should be used

VoxelMaterialType
-----------------

2 possible values:

* IgnoreMaterial: the material shouldn't be used
* UseMaterial: the material should be used