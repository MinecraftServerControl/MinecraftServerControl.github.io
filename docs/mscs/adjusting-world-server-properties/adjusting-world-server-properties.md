---
layout: default
title: Adjusting World & Server Properties
nav_order: 4
has_children: true
permalink: /docs/mscs/adjusting-world-server-properties
---

# Adjusting World & Server Properties
{: .no_toc }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Introduction

By default, every world in MSCS inherits from a global server properties file called `mscs.defaults`. These defaults can
be overidden on a per-world basis by creating an `mscs.properties` file in the directories of the world(s) you wish to
overwrite. Only properties that will be changed need to be copied into the `mscs.properties` file--the MSCS script will
use the global `mscs.defaults` for any properties that are left out.

What follows are the global server properties and individual world properties MSCS currently has available.
Additionally, we list examples of [common configuration settings](adjusting-world-server-properties#common-configuration-settings)
at the end of this page.

Examples of how to configure the properties for documented server mods can be found on the sidebar.

---

## Global Server Properties

The global server properties file is called `mscs.defaults`. As mentioned above, all MSCS worlds inherit properties from
this file unless the properties are overridden in the world's `mscs.properties` file.

This `mscs.defaults` file can be found at `/opt/mscs/mscs.defaults`.

When using the `msctl` script in multi-user mode, the `mscs.defaults` file can be found at either `$HOME/mscs.defaults`
or `$HOME/.config/mscs/mscs.defaults` (both are valid locations). Please note that `$HOME` represents the home directory
of the user that is running the script.

Listed below are the global server properties currently available. The properties that are set already are the defaults
that come with the script (properties that are empty have no defaults). You can change any of the properties to your
liking (including defaults) by adding them to the `mscs.defaults` file or editing them if they are already in the file.

```ini
; Location of the mscs files.
mscs-location=/opt/mscs

; Location of world files.
mscs-worlds-location=/opt/mscs/worlds

; URL to download the version_manifest.json file.
mscs-versions-url=https://launchermeta.mojang.com/mc/game/version_manifest.json

; Location of the version_manifest.json file.
mscs-versions-json=/opt/mscs/version_manifest.json

; Length in minutes to keep the version_manifest.json file before updating.
mscs-versions-duration=30

; Length in minutes to keep lock files before removing.
mscs-lockfile-duration=1440

; Properties to return for detailed listings.
mscs-detailed-listing=motd server-ip server-port max-players level-type online-mode

; Default world name.
mscs-default-world=world

; Default Port.
mscs-default-port=25565

; Default IP address. Leave this blank unless you want to bind all world
; servers to a single network interface by default.
mscs-default-ip=

; Default version type (release or snapshot).
mscs-default-version-type=release

; Default version of the client software. This sets the $CLIENT_VERSION
; variable. You can use the $CURRENT_VERSION variable to access the latest
; version based on the version type selected.
mscs-default-client-version=$CURRENT_VERSION

; Default .jar file for the client software. The $CLIENT_VERSION variable
; allows access to the client version selected.
mscs-default-client-jar=$CLIENT_VERSION.jar

; Default download URL for the client software. The $CLIENT_VERSION variable
; allows access to the client version selected.
mscs-default-client-url=

; Default location of the client .jar file. The $CLIENT_VERSION variable
; allows access to the client version selected.
mscs-default-client-location=/opt/mscs/.minecraft/versions/$CLIENT_VERSION

; Default version of the server software. This sets the $SERVER_VERSION
; variable. You can use the $CURRENT_VERSION variable to access the latest
; version based on the version type selected.
mscs-default-server-version=$CURRENT_VERSION

; Default arguments for the JVM. This sets the $JVM_ARGS variable.
mscs-default-jvm-args=

; Default .jar file for the server software. This sets the $SERVER_JAR
; variable. The $SERVER_VERSION variable allows access to the server version
; selected.
mscs-default-server-jar=minecraft_server.$SERVER_VERSION.jar

; Default download URL for the server software. The $SERVER_VERSION variable
; allows access to the server version selected.
mscs-default-server-url=

; Default arguments for a world server. This sets the $SERVER_ARGS variable.
mscs-default-server-args=nogui

; Default initial amount of memory for a world server. This sets the
; $INITIAL_MEMORY variable.
mscs-default-initial-memory=128M

; Default maximum amount of memory for a world server. This sets the
; $MAXIMUM_MEMORY variable.
mscs-default-maximum-memory=2048M

; Default location of the server .jar file. This sets the $SERVER_LOCATION
; variable.
mscs-default-server-location=/opt/mscs/server

; Default command to run for a world server. You can use the $JAVA variable to
; access the results of $(which java). The $INITIAL_MEMORY and $MAXIMUM_MEMORY
; variables provide access to the amounts of memory selected. The
; $SERVER_LOCATION and $SERVER_JAR variables provide access to the location
; and file name of the server software selected. The $JVM_ARGS variable
; provides access to the Java virtual machine arguments for the world server
; selected. The $SERVER_ARGS variable provides access to the server arguments
; for the world server selected.
mscs-default-server-command=$JAVA -Xms$INITIAL_MEMORY -Xmx$MAXIMUM_MEMORY $JVM_ARGS -jar $SERVER_LOCATION/$SERVER_JAR $SERVER_ARGS

; Default behavior if to restart the server after crash is detected (default disabled).
# mscs-default-restart-after-crash=false

; Location to store backup files.
mscs-backup-location=/opt/mscs/backups

; Location of the backup log file.
mscs-backup-log=/opt/mscs/backups/backup.log

; Files and directories excluded from backups. Each path is relative to the
; world/<world> directory. Separate each entry with commas.
mscs-backup-excluded-files=

; Length in days that backups survive. A value less than 1 disables backup deletion.
mscs-backup-duration=15

; Length in days that logs survive. A value less than 1 disables log deletion.
mscs-log-duration=15

; Enable the mirror option by default for worlds (default disabled). Change
; to a 1 to enable.
mscs-enable-mirror=0

; Default path for the mirror files.
mscs-mirror-path=/dev/shm/mscs

; Location of Overviewer.
mscs-overviewer-bin=/usr/bin/overviewer.py

; URL for Overviewer.
mscs-overviewer-url=http://overviewer.org

; Location of Overviewer generated map files.
mscs-maps-location=/opt/mscs/maps

; URL for accessing Overviewer generated maps.
mscs-maps-url=http://minecraft.server.com/maps
```

The following variables may be used in some of the above properties:

- `$JAVA` - The Java virtual machine (`which java`).
- `$CURRENT_VERSION` - The current Mojang Minecraft release version.
- `$CLIENT_VERSION` - The version of the client software.
- `$SERVER_VERSION` - The version of the server software.
- `$JVM_ARGS` - The arguments to the JVM.
- `$SERVER_JAR` - The .jar file to run for the server.
- `$SERVER_ARGS` - The arguments to the server.
- `$INITIAL_MEMORY` - The initial amount of memory for the server.
- `$MAXIMUM_MEMORY` - The maximum amount of memory for the server.
- `$SERVER_LOCATION` - The location of the server .jar file.
- `$WORLD_NAME` - The name of the world.

---

## Individual World Properties

As mentioned earlier, each world server can override the default, global server values by adding properties to the
world's `mscs.properties` file. The `mscs.properties` file can be found in every world folder (for instance, if you had
a world called `myWorld`, the path would be `/opt/mscs/worlds/myWorld/mscs.properties`).

Listed below are the individual world properties currently available. The properties that are set already are the
defaults that come with the script (properties that are empty have no defaults). You can change any of the properties to
your liking (including defaults) by adding them to the `mscs.properties` file or editing them if they are already in
the file.

```ini
; Enable or disable the world server.
mscs-enabled=true

; Assign the version type (release or snapshot).
mscs-version-type=release

; Assign the version of the client software. This sets the $CLIENT_VERSION
; variable. You can use the $CURRENT_VERSION variable to access the latest
; version based on the version type selected.
mscs-client-version=$CURRENT_VERSION

; Assign the .jar file for the client software. The $CLIENT_VERSION variable
; allows access to the client version selected.
mscs-client-jar=$CLIENT_VERSION.jar

; Assign the download URL for the client software. The $CLIENT_VERSION variable
; allows access to the client version selected.
mscs-client-url=https://s3.amazonaws.com/Minecraft.Download/versions/$CLIENT_VERSION/$CLIENT_VERSION.jar

; Assign the location of the client .jar file. The $CLIENT_VERSION variable
; allows access to the client version selected.
mscs-client-location=/opt/mscs/.minecraft/versions/$CLIENT_VERSION

; Assign the version of the server software. This sets the $SERVER_VERSION
; variable. You can use the $CURRENT_VERSION variable to access the latest
; version based on the version type selected.
mscs-server-version=$CURRENT_VERSION

; Assign the arguments to the JVM. This sets the $JVM_ARGS variable.
mscs-jvm-args=

; Assign the .jar file for the server software. This sets the $SERVER_JAR
; variable. The $SERVER_VERSION variable allows access to the server version
; selected.
mscs-server-jar=minecraft_server.$SERVER_VERSION.jar

; Assign the download URL for the server software. The $SERVER_VERSION variable
; allows access to the server version selected.
mscs-server-url=https://s3.amazonaws.com/Minecraft.Download/versions/$SERVER_VERSION/minecraft_server.$SERVER_VERSION.jar

; Assign the arguments to the server. This sets the $SERVER_ARGS variable.
mscs-server-args=nogui

; Assign the initial amount of memory for the server. This sets the
; $INITIAL_MEMORY variable.
mscs-initial-memory=128M

; Assign the maximum amount of memory for the server. This sets the
; $MAXIMUM_MEMORY variable.
mscs-maximum-memory=2048M

; Assign the location of the server .jar file. This sets the $SERVER_LOCATION
; variable.
mscs-server-location=/opt/mscs/server

; Assign the command to run for the server. You can use the $JAVA variable to
; access the results of $(which java). The $INITIAL_MEMORY and $MAXIMUM_MEMORY
; variables provide access to the amounts of memory selected. The
; $SERVER_LOCATION and $SERVER_JAR variables provide access to the location
; and file name of the server software selected. The $JVM_ARGS variable
; provides access to the Java virtual machine arguments for the world server
; selected. The $SERVER_ARGS variable provides access to the server arguments
; for the world server selected.
mscs-server-command=$JAVA -Xms$INITIAL_MEMORY -Xmx$MAXIMUM_MEMORY $JVM_ARGS -jar $SERVER_LOCATION/$SERVER_JAR $SERVER_ARGS

; Restart the server after a crash (default disabled).
mscs-restart-after-crash=false
```

The following variables may be used in some of the values of the above keys:

- `$JAVA` - The Java virtual machine.
- `$CURRENT_VERSION` - The current Mojang Minecraft release version.
- `$CLIENT_VERSION` - The version of the client software.
- `$SERVER_VERSION` - The version of the server software.
- `$JVM_ARGS` - The arguments to the JVM.
- `$SERVER_JAR` - The .jar file to run for the server.
- `$SERVER_ARGS` - The arguments to the server.
- `$INITIAL_MEMORY` - The initial amount of memory for the server.
- `$MAXIMUM_MEMORY` - The maximum amount of memory for the server.
- `$SERVER_LOCATION` - The location of the server .jar file.

---

## Common Configuration Settings

The examples below assumes you are editing the world's `mscs.properties`.

### Set World's Server Version

Use a specific release:

```ini
mscs-server-version=1.14
mscs-client-version=1.14
```

Use the latest snapshot:

```ini
mscs-version-type=snapshot
```

Use a specific snapshot:

```ini
mscs-version-type=snapshot
mscs-client-version=14w11b
mscs-server-version=14w11b
```

### Set World's Memory

```ini
# Assign the initial amount of memory for the server.
mscs-initial-memory=128M

# Assign the maximum amount of memory for the server.
mscs-maximum-memory=2048M
```

### Set World's Logging Setting

Want to customize the server logs? You can configure log4j by setting
`mscs-jvm-args`.

Example setting:

```ini
mscs-jvm-args=-Dlog4j.configurationFile=/opt/mscs/log4j2.xml
```

### Set World's Custom Java Command

Do you want a crazy Java command? You can do it with `mscs-server-command`:

```ini
mscs-server-command=$JAVA -Xms$INITIAL_MEMORY -Xmx$MAXIMUM_MEMORY -Xincgc -XX:NewRatio=3 -XX:+UseThreadPriorities -XX:CMSFullGCsBeforeCompaction=1 -XX:SoftRefLRUPolicyMSPerMB=2048 -XX:+CMSParallelRemarkEnabled -XX:+UseParNewGC -XX:+UseAdaptiveSizePolicy -XX:+DisableExplicitGC -Xnoclassgc -oss4M -ss4M -XX:+UseFastAccessorMethods -XX:CMSInitiatingOccupancyFraction=90 -XX:+UseConcMarkSweepGC -XX:UseSSE=4 -XX:+UseCMSCompactAtFullCollection -XX:ParallelGCThreads=8 -XX:+AggressiveOpts -Djava.awt.headless=true -jar $SERVER_LOCATION/$SERVER_JAR $SERVER_ARGS
```

Yes, this command could be used... but we do not guarantee that it will work or that it will make a server any faster/better/harder/stronger.
