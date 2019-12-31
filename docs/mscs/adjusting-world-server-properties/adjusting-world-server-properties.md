---
layout: default
title: Adjusting world & server properties
nav_order: 4
has_children: true
permalink: /docs/mscs/adjusting-world-server-properties
---

# Adjusting world & server properties
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Introduction
By default, every world in MSCS inherits from a global server properties file called `mscs.defaults`. 
These defaults can be overidden on a per-world basis by creating an `mscs.properties` file in the directories of the
world(s) you wish to overwrite. Only properties that will be changed need to be copied into the `mscs.properties` file--the MSCS script will use the global `mscs.defaults` for any properties that are left out.

Instructions to configure the properties for major server mods can be found on the sidebar--specifically [PaperMC](https://minecraftservercontrol.github.io/docs/mscs/adjusting-world-server-properties/papermc),
[SpigotMC](https://minecraftservercontrol.github.io/docs/mscs/adjusting-world-server-properties/spigotmc), [Forge](https://minecraftservercontrol.github.io/docs/mscs/adjusting-world-server-properties/forge), [BungeeCord](https://minecraftservercontrol.github.io/docs/mscs/adjusting-world-server-properties/bungeecord), and [Technic/Tekkit Pack](https://minecraftservercontrol.github.io/docs/mscs/adjusting-world-server-properties/technic-tekkit-pack). 
Additionally, we list examples of [common configuration settings at the end of this document](https://minecraftservercontrol.github.io/docs/mscs/adjusting-world-server-properties#common-configuration-settings).

---

## Global server properties
The global server properties file is called `mscs.defaults`. As mentioned
above, all MSCS worlds inherit properties from this file unless the properties
are overridden in the world's `mscs.properties` file. 

This `mscs.defaults` file can be found at
`/opt/mscs/mscs.defaults`. 

When using the `msctl` script in multi-user mode,
the `mscs.defaults` file can be found at either `$HOME/mscs.defaults` or
`$HOME/.config/mscs/mscs.defaults` (both are valid locations).
Please note that `$HOME` represents the 
home directory of the user that is running the script.

Listed below are the global server properties currently available. The properties that are set
already are the defaults that come with the script (properties that are empty
have no defaults). You can change any of the properties to your liking (including defaults) by adding them
to the `mscs.defaults` file or editing them if they are already in the file. 

    # Location of the mscs files.
    mscs-location=/opt/mscs

    # Location of world files.
    mscs-worlds-location=/opt/mscs/worlds

    # URL to download the version_manifest.json file.
    mscs-versions-url=https://launchermeta.mojang.com/mc/game/version_manifest.json

    # Location of the version_manifest.json file.
    mscs-versions-json=/opt/mscs/version_manifest.json

    # Length in minutes to keep the version_manifest.json file before updating.
    mscs-versions-duration=30

    # Length in minutes to keep lock files before removing.
    mscs-lockfile-duration=1440

    # Default world name.
    mscs-default-world=world

    # Default Port.
    mscs-default-port=25565

    # Default IP address.
    mscs-default-ip=

    # Default version type (release or snapshot).
    mscs-default-version-type=release

    # Default version of the client software.
    mscs-default-client-version=$CURRENT_VERSION

    # Default .jar file for the client software.
    mscs-default-client-jar=$CLIENT_VERSION.jar

    # Default download URL for the client software.
    mscs-default-client-url=

    # Default download URL for the client software.
    mscs-default-client-location=/opt/mscs/.minecraft/versions/$CLIENT_VERSION

    # Default version of the server software.
    mscs-default-server-version=$CURRENT_VERSION

    # Default arguments for the JVM.
    mscs-default-jvm-args=

    # Default .jar file for the server software.
    mscs-default-server-jar=minecraft_server.$SERVER_VERSION.jar

    # Default download URL for the server software.
    mscs-default-server-url=

    # Default arguments for a world server.
    mscs-default-server-args=nogui

    # Default initial amount of memory for a world server.
    mscs-default-initial-memory=128M

    # Default maximum amount of memory for a world server.
    mscs-default-maximum-memory=2048M

    # Default location of the server .jar file.
    mscs-default-server-location=/opt/mscs/server

    # Default command to run for a world server.
    mscs-default-server-command=$JAVA -Xms$INITIAL_MEMORY -Xmx$MAXIMUM_MEMORY -jar $SERVER_LOCATION/$SERVER_JAR $SERVER_ARGS

    # Location to store backup files.
    mscs-backup-location=/opt/mscs/backups

    # Location of the backup log file.
    mscs-backup-log=/opt/mscs/backups/backup.log

    # Length in days that backups survive. A value less than 1 disables backup deletion.
    mscs-backup-duration=15

    # Length in days that logs survive. A value less than 1 disables log deletion.
    mscs-log-duration=15

    # Properties to return for detailed listings.
    mscs-detailed-listing=motd server-ip server-port max-players level-type online-mode

    # Enable the mirror option by default for worlds.
    # 0 = disabled (default), 1 = enabled.
    mscs-enable-mirror=0

    # Default path for the mirror files.
    mscs-mirror-path=/dev/shm/mscs

    # Location of Overviewer.
    mscs-overviewer-bin=/usr/bin/overviewer.py

    # URL for Overviewer.
    mscs-overviewer-url=http://overviewer.org

    # Location of Overviewer generated map files.
    mscs-maps-location=/opt/mscs/maps

    # URL for accessing Overviewer generated maps.
    mscs-maps-url=http://minecraft.server.com/maps
    
The following variables may be used in some of the above properties:
* $JAVA                - The Java virtual machine.
* $CURRENT_VERSION     - The current Mojang Minecraft release version.
* $CLIENT_VERSION      - The version of the client software.
* $SERVER_VERSION      - The version of the server software.
* $JVM_ARGS            - The arguments to the JVM.
* $SERVER_JAR          - The .jar file to run for the server.
* $SERVER_ARGS         - The arguments to the server.
* $INITIAL_MEMORY      - The initial amount of memory for the server.
* $MAXIMUM_MEMORY      - The maximum amount of memory for the server.
* $SERVER_LOCATION     - The location of the server .jar file.

---

## Individual world properties
As mentioned earlier, each world server can override the default, global server values by
adding properties to the world's `mscs.properties` file. The
`mscs.properties` file can be found in every world folder (for instance, if
you had a world called `myWorld`, the path would be
`/opt/mscs/worlds/myWorld/mscs.properties`). 

Listed below are the individual world properties currently available. The properties that are set
already are the defaults that come with the script (properties that are empty
have no defaults). You can change any of the properties to your liking (including defaults) by adding them
to the `mscs.properties` file or editing them if they are already in the file. 

    # Enable or disable the world server.
    mscs-enabled=true

    # Assign the version type (release or snapshot).
    mscs-version-type=release

    # Assign the version of the client software.
    mscs-client-version=$CURRENT_VERSION

    # Assign the .jar file for the client software.
    mscs-client-jar=$CLIENT_VERSION.jar

    # Assign the download URL for the client software.
    mscs-client-url=https://s3.amazonaws.com/Minecraft.Download/versions/$CLIENT_VERSION/$CLIENT_VERSION.jar

    # Assign the location of the client .jar file.
    mscs-client-location=/opt/mscs/.minecraft/versions/$CLIENT_VERSION

    # Assign the version of the server software.
    mscs-server-version=$CURRENT_VERSION

    # Assign the arguments to the JVM.
    mscs-jvm-args=

    # Assign the .jar file for the server software.
    mscs-server-jar=minecraft_server.$SERVER_VERSION.jar

    # Assign the download URL for the server software.
    mscs-server-url=https://s3.amazonaws.com/Minecraft.Download/versions/$SERVER_VERSION/minecraft_server.$SERVER_VERSION.jar

    # Assign the arguments to the server.
    mscs-server-args=nogui

    # Assign the initial amount of memory for the server.
    mscs-initial-memory=128M

    # Assign the maximum amount of memory for the server.
    mscs-maximum-memory=2048M

    # Assign the location of the server .jar file.
    mscs-server-location=/opt/mscs/server

    # Assign the command to run for the server.
    mscs-server-command=$JAVA -Xms$INITIAL_MEMORY -Xmx$MAXIMUM_MEMORY -jar $SERVER_LOCATION/$SERVER_JAR $SERVER_ARGS
    
The following variables may be used in some of the values of the above keys:
* $JAVA - The Java virtual machine.
* $CURRENT_VERSION - The current Mojang Minecraft release version.
* $CLIENT_VERSION - The version of the client software.
* $SERVER_VERSION - The version of the server software.
* $SERVER_JAR - The .jar file to run for the server.
* $SERVER_ARGS - The arguments to the server.
* $INITIAL_MEMORY - The initial amount of memory for the server.
* $MAXIMUM_MEMORY - The maximum amount of memory for the server.
* $SERVER_LOCATION - The location of the server .jar file.

---

## Common configuration settings

### Set the server version

### Set memory
