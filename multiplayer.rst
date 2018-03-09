Multiplayer
===========

For now, multiplayer works with IPv4 sockets, which means that the server must have a public IPv4, and that port forwarding must be configured.

**All the edits must be made on the server**, as the plugin is just sending the diffs from the server to the clients.

To enable multiplayer, tick the **Multiplayer** property of the Voxel World.

As custom sockets are used, you must call **Connect Client** and **Start Server** functions manually.

Due to how collisions are handled in the plugin, you must make your Character inherit of **VoxelCharacter**. Expect random TPs if you don't do so.

Connect Client
--------------

.. raw:: html
   :file: generated_doc/ConnectClient.html

Start Server
------------

.. raw:: html
   :file: generated_doc/StartServer.html

