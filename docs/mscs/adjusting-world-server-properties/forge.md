---
layout: default
title: Forge
nav_order: 3
parent: Adjusting world & server properties
permalink: /docs/mscs/adjusting-world-server-properties/forge
---

# Forge
[Forge](http://www.minecraftforge.net/) has an easy to use installer that can be used to install all of the needed files to run a Forge server, starting with version `1.6.2-9.10.0.818`. To install a version compatible with Minecraft 1.8.9, [download](http://files.minecraftforge.net/) the Forge installer `forge-x.x-xx.xx.x.xxxx-installer` and run the following as the `minecraft` user (`sudo su minecraft`):

    cd /opt/mscs/server
    wget http://files.minecraftforge.net/maven/net/minecraftforge/forge/1.8.9-11.15.1.1722/forge-1.8.9-11.15.1.1722-installer.jar
    java -jar forge-1.8.9-11.15.1.1722-installer.jar --installServer

The installer should install the forge server jar to `/opt/mscs/server/forge-1.8-11.14.2.1434-universal.jar` and a bunch of library files in `/opt/mscs/server/libraries/`.

Create a new server (if necessary):

    mscs create forge 25565

`forge` can be replaced with any name. Ensure that port `25565` is an unused port, or change it if nessessary.

This will create the directory `forge` in `/opt/mscs/worlds` as well as the `server.properties` and `mscs.properties` files:

Change the directory to the world that was created:

    cd /opt/mscs/worlds/forge

Modify the `mscs.properties` file and add/alter these lines, replacing versions and file paths as needed:

    mscs-client-version=1.8.4
    mscs-server-version=1.8.4
    mscs-server-jar=forge-1.8.9-11.15.1.1722-universal.jar
    mscs-server-url=

Start the server:

    mscs start forge

If the server fails to start, the `eula.txt` file may need to be edited and accepted:

    editor /opt/mscs/worlds/forge/eula.txt

The server should start up and run  
The server startup can be monitored by running:

    mscs console forge

Once you are done watching the server boot up, you can press `<Ctrl-D>` to detach.

Simply add mods as you would normally by dragging them into the `/opt/mscs/worlds/forge/mods` folder,
assuming `forge` is the name of your world.
