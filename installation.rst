Installation
============

Manual installation
-------------------

* In your game’s root directory, create a folder named Plugins
* Copy the Voxel folder into it. You should have something like::

    MyProject
    ├── Content
    └── Plugins
        └── Voxel
            └── Voxel.uplugin

* If you want to use it in your C++ project: add **"Voxel"** as public dependency in **MyProject.Build.cs**. You should have ::
    
    PublicDependencyModuleNames.AddRange(new string[] { "Core", "CoreUObject", "Engine", "InputCore", "Voxel" });
