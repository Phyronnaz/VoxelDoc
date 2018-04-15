Installation
============

Manual installation
-------------------

They are 2 versions of the plugin: 4.XX.XX, and 4.XX.XX-TextureArrays. To use the TextureArrays one, you need to use a custom build of the engine: see :doc:`texturearrays` for more info

* In your game’s root directory, create a folder named Plugins
* Copy the Voxel folder into it. You should have something like::

    MyProject
    ├── Content
    └── Plugins
        └── Voxel
            └── Voxel.uplugin

* If you want to use it in your C++ project: add **"Voxel"** as public dependency in **MyProject.Build.cs**. You should have ::
    
    PublicDependencyModuleNames.AddRange(new string[] { "Core", "CoreUObject", "Engine", "InputCore", "Voxel" });

.. raw:: html

    <div class="video-container"><iframe src="https://www.youtube.com/embed/EpXu9kqFoSM?rel=0" frameborder="0" allowfullscreen></iframe></div>
    
.. raw:: html

	<p></p>
