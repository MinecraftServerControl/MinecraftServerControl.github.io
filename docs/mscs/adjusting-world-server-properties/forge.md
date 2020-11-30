---
layout: default
title: Forge
nav_order: 3
parent: Adjusting World & Server Properties
permalink: /docs/mscs/adjusting-world-server-properties/forge
---

# Forge

[Forge][forge] has an easy to use installer that can be used to install all of the needed files to run a Forge server.
To install a version compatible with Minecraft 1.16.4, [download][download] the Forge installer `forge-forge-x.x.x-x.x.x-installer`
and run the following as the `minecraft` user (`sudo su minecraft`):

```bash
mkdir -p /opt/mscs/server/forge-1.16.4-35.1.7
cd /opt/mscs/server/forge-1.16.4-35.1.7
wget https://files.minecraftforge.net/maven/net/minecraftforge/forge/1.16.4-35.1.7/forge-1.16.4-35.1.7-installer.jar
java -jar forge-1.16.4-35.1.7-installer.jar --installServer
```

The installer should install the forge server jar to `/opt/mscs/server/forge-1.16.4-35.1.7/forge-1.16.4-35.1.7.jar`
and a bunch of library files in `/opt/mscs/server/forge-1.16.4-35.1.7/libraries/`.

Create a new server (if necessary):

```bash
mscs create forge 25565
```

`forge` can be replaced with any name. Ensure that port `25565` is an unused port, or change it if nessessary.

This will create the directory `forge` in `/opt/mscs/worlds` as well as the `server.properties` and `mscs.properties`
files:

Change the directory to the world that was created:

```bash
cd /opt/mscs/worlds/forge
```

Modify the `mscs.properties` file and add/alter these lines, replacing versions and file paths as needed:

```bash
editor /opt/mscs/worlds/forge/mscs.properties
```

Add this

```ini
mscs-client-version=1.16.4
mscs-server-version=1.16.4
mscs-server-jar=forge-1.16.4-35.1.7/forge-1.16.4-35.1.7.jar
mscs-server-url=
```

You may also want to increase the initial RAM and possibly even the maximum RAM.

> Minimum default is 128M  
> Maximum default is 2048M

```ini
mscs-initial-memory=1024M
mscs-maximum-memory=3048M
```

If the server fails to start, the `eula.txt` file may need to be edited and accepted:

```bash
editor /opt/mscs/worlds/forge/eula.txt
```

Change `false` to `true`

```ini
eula=true
```

Stop then Start the server:

```bash
mscs stop forge
mscs start forge
```

The server should start up and run

The server startup can be monitored by running:

```bash
mscs watch forge
```

Once you are done watching the server boot up, you can press `<Ctrl-C>` to detach.

Simply add mods as you would normally by dragging them into the `/opt/mscs/worlds/forge/mods` folder, assuming `forge`
is the name of your world.

[forge]: http://www.minecraftforge.net
[download]: http://files.minecraftforge.net
