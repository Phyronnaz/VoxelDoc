=====================
Materials Collections
=====================

----
Goal
----

The goal of materials collections is to automatically generate materials that blend multiple materials.

It takes in input a list of materials, and outputs three lists:

* a list of **Single** materials: this is the same as the input list
* a list of **Double** materials: for every pair of input materials,
  creates a material blending them according to the vertex color input
* a list of **Triple** materials: for every triplet of input materials,
  creates a material blending them according to the vertex color input

-----
Usage
-----

You have a list of master materials & material instances that you want to convert to a material collection.

.. note::
    You can have only master materials, however using material instances is highly suggested to improve shader compilation time.

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Converting master materials to material functions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

First of all, you need to convert your master materials to material functions.
To do that:

* Create a new material function
* Add a **MakeMaterialAttributes** node
* Connect it to the function output
* Copy all the nodes of your master material inside this function, and link the material attributes accordingly

.. hint::
    To avoid code duplication, you should remove all the nodes of your master material and replace them by this new function.
    You'll need to tick the **Use Material Attributes** checkbox in the material settings.

^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Creating the material collection
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You now need to create & setup your material collection:

* Create a new voxel material collection using the content browser context menu
* Leave the templates to their default values
* For each master material, add a new material to the **Materials** array under the *Layers* category
  and set its value to the material function you created above
* If your master material has instances:

  * Expand the array element you just added using the arrow on the left
  * Add new instances to the **Instances** array
* Once all your materials/instances have been added, you need to set their indices using the input boxes on the left
* If you want to generate tessellated versions of your materials, tick the **Enable Tessellation** property under the *General* category.

.. hint::
    If you don't need custom physical materials, you can tick the **Hide Physical Materials** property under the *General* category.

^^^^^^^^^^^^^^^^^^^^^^^^
Generating the materials
^^^^^^^^^^^^^^^^^^^^^^^^

You can now click the **Generate Single** button.
This will generate the single materials, which should be enough for basic testing.

Once you're happy with the look of your materials,
you can generate the double & triple ones using the **Generate Double** and **Generate Triple** buttons.

.. note::
    Changes to the original materials/instances won't be propagated to the generated ones.
    You'll need to generate them again!

^^^^^^^^^^^^^^^^^^
Suggested workflow
^^^^^^^^^^^^^^^^^^

Convert your master materials to material functions as described above.
Fine tune them without using the material collection,
and once you're happy with their look, generate the generated materials.
You should try to minimize the number of generations as much as possible due to their high shader compile time.

^^^^^^^^^^^^^^^^^^^^^^^^^^
Performance considerations
^^^^^^^^^^^^^^^^^^^^^^^^^^

The number of generated materials is exponential in the number of master materials.
To reduce the number of shaders to compile, you should use material instances as much as possible.
