---
layout: default
title: Adjusting world & server properties
nav_order: 4
permalink: /docs/mscs/adjusting-world-server-properties
---

# Adjusting world & server properties
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

By default, every world in MSCS inherits from a global server properties file called `mscs.defaults`. 
These defaults can be overidden on a per-world basis by creating an `mscs.properties` file in the directories of the
world(s) you wish to overwrite. Only properties that will be changed need to be copied into the `mscs.properties` file--
the MSCS script will use the global `mscs.defaults` for any properties that are left out.

---

## Global server properties
The global server properties file is called `mscs.defaults`. This file can be found at
`/opt/mscs/mscs.defaults`. When using the `msctl` script in multi-user mode,
the `mscs.defaults` file can be found at either `$HOME/mscs.defaults` or
`$HOME/.config/mscs/mscs.defaults`.

Listed below are the global server properties currently available. The properties that are set
already are the defaults that come with the script (properties that are empty
have no defaults). You can change any of the properties to your liking (including defaults) by adding them
to the `mscs.defaults` file or editing them if they are already in the file. 

    mscs-location=/opt/mscs
    mscs-worlds-location=/opt/mscs/worlds
    mscs-versions-url=https://launchermeta.mojang.com/mc/game/version_manifest.json
    mscs-versions-json=/opt/mscs/version_manifest.json
    mscs-versions-duration=30
    mscs-lockfile-duration=1440
    mscs-default-world=world
    mscs-default-port=25565
    mscs-default-ip=
    mscs-default-version-type=release
    mscs-default-client-version=$CURRENT_VERSION
    mscs-default-client-jar=$CLIENT_VERSION.jar
    mscs-default-client-url=
    mscs-default-client-location=/opt/mscs/.minecraft/versions/$CLIENT_VERSION
    mscs-default-server-version=$CURRENT_VERSION
    mscs-default-jvm-args=
    mscs-default-server-jar=minecraft_server.$SERVER_VERSION.jar
    mscs-default-server-url=
    mscs-default-server-args=nogui
    mscs-default-initial-memory=128M
    mscs-default-maximum-memory=2048M
    mscs-default-server-location=/opt/mscs/server
    mscs-default-server-command=$JAVA -Xms$INITIAL_MEMORY -Xmx$MAXIMUM_MEMORY -jar $SERVER_LOCATION/$SERVER_JAR $SERVER_ARGS
    mscs-backup-location=/opt/mscs/backups
    mscs-backup-log=/opt/mscs/backups/backup.log
    mscs-backup-duration=15
    mscs-log-duration=15
    mscs-detailed-listing=motd server-ip server-port max-players level-type online-mode
    mscs-enable-mirror=0
    mscs-mirror-path=/dev/shm/mscs
    mscs-overviewer-bin=/usr/bin/overviewer.py
    mscs-overviewer-url=http://overviewer.org
    mscs-maps-location=/opt/mscs/maps
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
Each world server can override the default, global server values by
adding properties to the world's `mscs.properties` file. The
`mscs.properties` file can be found in every world folder (for instance, if
you had a world called `myWorld`, the path would be
`/opt/mscs/worlds/myWorld/mscs.properties`). 

Listed below are the individual world properties currently available. The properties that are set
already are the defaults that come with the script (properties that are empty
have no defaults). You can change any of the properties to your liking (including defaults) by adding them
to the `mscs.properties` file or editing them if they are already in the file. 

    mscs-enabled=true
    mscs-version-type=release
    mscs-client-version=$CURRENT_VERSION
    mscs-client-jar=$CLIENT_VERSION.jar
    mscs-client-url=https://s3.amazonaws.com/Minecraft.Download/versions/$CLIENT_VERSION/$CLIENT_VERSION.jar
    mscs-client-location=/opt/mscs/.minecraft/versions/$CLIENT_VERSION
    mscs-server-version=$CURRENT_VERSION
    mscs-jvm-args=
    mscs-server-jar=minecraft_server.$SERVER_VERSION.jar
    mscs-server-url=https://s3.amazonaws.com/Minecraft.Download/versions/$SERVER_VERSION/minecraft_server.$SERVER_VERSION.jar
    mscs-server-args=nogui
    mscs-initial-memory=128M
    mscs-maximum-memory=2048M
    mscs-server-location=/opt/mscs/server
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
