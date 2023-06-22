---
layout: default
title: Fabric
nav_order: 2
parent: Adjusting World & Server Properties
permalink: /docs/mscs/adjusting-world-server-properties/fabric
---

# Fabric

This guide describes how to configure MSCS to run a world using [Fabric][fabric].

There are several ways to install Fabric.
This document describes the current recommended method,
which uses an executable [server launcher][launcher] instead of a separate installer.
Manual installation using an [installer JAR][installer] is not covered.

## Initial configuration

1. [Download the server launcher][launcher] into the Minecraft Server Control Script's server directory.

   Note: the URL in the following example will not work.
   You must use the `curl` command provided on the download page.
   ```
   cd /opt/mscs/server
   curl -OJ https://meta.fabricmc.net/v2/versions/loader/GameVersion/LoaderVersion/InstallerVersion/server/jar
   ```
2. When the download completes, it will tell you the filename that was saved.
   Take note of it (or copy it to your clipboard) for use in a future step.

   Continuing the artificial (non-functional) example from the previous step...
   ```
   $ curl -OJ https://meta.fabricmc.net/v2/versions/loader/GameVersion/LoaderVersion/InstallerVersion/server/jar
     % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                    Dload  Upload   Total   Spent    Left  Speed
   100  143k    0  143k    0     0   109k      0 --:--:--  0:00:01 --:--:--  109k
   curl: Saved to filename 'fabric-server-mc.GameVersion-loader.LoaderVersion-launcher.LauncherVersion.jar'
   ```
3. Create a world.
   (Replace "fabric-example" with your desired world name here and in future steps.)
   ```
   mscs create fabric-example
   ```
4. Configure the world to use the Fabric JAR by configuring some settings in `mscs.properties`.

   Note: this uses the filename from the artificial example above.
   When you run the first command, you must use the filename that you observed in step 2 instead of this example's artificial filename.
   ```
   echo 'mscs-server-jar=fabric-server-mc.GameVersion-loader.LoaderVersion-launcher.LauncherVersion.jar' >> /opt/mscs/worlds/fabric-example/mscs.properties
   echo 'mscs-server-url=' >> /opt/mscs/worlds/fabric-example/mscs.properties
   ```
5. Accept the EULA.
   ```
   echo 'eula=true' > /opt/mscs/worlds/fabric-example/eula.txt
   ```
6. (optional) Customize your world's settings in `mscs.properties` and `server.properties`.
   See [Adjusting World & Server Properties](/docs/mscs/adjusting-world-server-properties) to learn about MSCS-specific settings.
   The Minecraft Wiki documents [the settings that are configurable in `server.properties`][server.properties].
7. Start the server.
   ```
   mscs start fabric-example
   ```

## Updating
To update, repeat steps 1 and 2 above.
Then, change `mscs-server-jar` in your world's `mscs.properties` to the updated version's filename.
Finally, restart your world.

[fabric]: https://fabricmc.net
[launcher]: https://fabricmc.net/use/server/
[installer]: https://fabricmc.net/wiki/player:tutorials:install_server
[server.properties]: https://minecraft.fandom.com/wiki/Server.properties
