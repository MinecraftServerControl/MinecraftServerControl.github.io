---
layout: default
title: QuiltMC
nav_order: 6
parent: Adjusting World & Server Properties
permalink: /docs/mscs/adjusting-world-server-properties/quiltmc
---

# QuiltMC

[QuiltMC][quiltmc] has an easy to use installer that can be used to install all of the needed files to run a QuiltMC server. [Download][download] the QuiltMC installer `quilt-installer-x.x.x.jar` and run the following as the `minecraft` user (`sudo su minecraft`)

```bash
mkdir -p /opt/mscs/server/quilt-{MINECRAFT_VERSION}
cd /opt/mscs/server/quilt-{MINECRAFT_VERSION}
wget {URL_TO_QUILT_INSTALLER}
java -jar quilt-installer-{INSTALLER_VERSION}.jar \
  install server {MINECRAFT_VERSION} \
  --download-server
```

> Replace `{INSTALLER_VERSION}` and `{MINECRAFT_VERSION}` as needed.

The installer should install the QuiltMC server jar to `/opt/mscs/server/quilt-{MINECRAFT_VERSION}/quilt-server-launch.jar`
and a bunch of library files in `/opt/mscs/server/quilt-{MINECRAFT_VERSION}/libraries/`.

Create a new server (if necessary):

```bash
mscs create quiltmc 25565
```

`quiltmc` can be replaced with any name. Ensure that port `25565` is an unused port, or change it if nessessary.

This will create the directory `quiltmc` in `/opt/mscs/worlds` as well as the `server.properties` and `mscs.properties`
files:

Change the directory to the world that was created:

```bash
cd /opt/mscs/worlds/quiltmc
```

Modify the `mscs.properties` file and add/alter these lines, replacing versions and file paths as needed:

```bash
editor /opt/mscs/worlds/quiltmc/mscs.properties
```

Add this

```ini
mscs-client-version={MINECRAFT_VERSION}
mscs-server-version={MINECRAFT_VERSION}
mscs-server-jar=quilt-{MINECRAFT_VERSION}/quilt-server-launch.jar
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
editor /opt/mscs/worlds/quiltmc/eula.txt
```

Change `false` to `true`

```ini
eula=true
```

Stop then Start the server:

```bash
mscs stop quiltmc
mscs start quiltmc
```

The server should start up and run

The server startup can be monitored by running:

```bash
mscs watch quiltmc
```

Once you are done watching the server boot up, you can press `<Ctrl-C>` to detach.

Simply add mods as you would normally by dragging them into the `/opt/mscs/worlds/quiltmc/mods` folder, assuming `quiltmc`
is the name of your world.


[quiltmc]: https://quiltmc.org/en/
[download]: https://quiltmc.org/en/install/server/
