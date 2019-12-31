---
layout: default
title: SpigotMC 
nav_order: 2
parent: Adjusting world & server properties
permalink: /docs/mscs/adjusting-world-server-properties/spigotmc
---

# SpigotMC
Installing [SpigotMC](https://www.spigotmc.org/wiki/spigot/) is very similar to installing Forge. Change to the `/opt/mscs/server/` directory, [download](https://hub.spigotmc.org/jenkins/job/BuildTools/) the SpigotMC installer `BuildTools.jar`, and run the following as the `minecraft` user (`sudo su minecraft`):

    cd /opt/mscs/server
    wget https://hub.spigotmc.org/jenkins/job/BuildTools/lastSuccessfulBuild/artifact/target/BuildTools.jar
    java -jar BuildTools.jar

This will build the `spigot-X.X.X.jar` server file.

Create a new server (if necessary):

    mscs create spigot 25565

`spigot` can be replaced with any name. Ensure that port `25565` is an unused port, or change it if nessessary.

This will create the directory `spigot` in `/opt/mscs/worlds` as well as the `server.properties` and `mscs.properties` files:

Change the directory to the world that was created:

    cd /opt/mscs/worlds/spigot

Modify the `mscs.properties` file and add/alter these lines, replacing versions and file paths as needed. You will
need to change the `mscs-server-jar` as a bare minimum:

    mscs-client-version=1.8.7
    mscs-server-version=1.8.7
    mscs-server-jar=spigot-1.8.7.jar
    mscs-server-url=

Start the server:

    mscs start spigot

If the server fails to start, the `eula.txt` file may need to be edited and accepted:

    editor /opt/mscs/worlds/spigot/eula.txt

The server should start up and run  
The server startup can be monitored by running:

    mscs console spigot

Once you are done watching the server boot up, you can press `<Ctrl-D>` to detach.

Simply add plugins as you would normally by dragging them into the `/opt/mscs/worlds/spigot/plugins` folder,
assuming `spigot` is the name of your world.
