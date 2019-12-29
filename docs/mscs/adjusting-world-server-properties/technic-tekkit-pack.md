---
layout: default
title: Technic/Tekkit Pack
nav_order: 6
parent: Adjusting world & server properties
permalink: /docs/mscs/adjusting-world-server-properties/technic-tekkit-pack
---

# Technic/Tekkit Pack
This example was written for [Attack of the B-Team](http://www.technicpack.net/modpack/attack-of-the-bteam.552556) version 1.0.9c

This works for many of the Technic/Tekkit based modpacks, although some settings may need to be adjusted for different modpacks.

Create the world:

    mscs create bteam 25565

`bteam` can be replaced with any name. Ensure that port `25565` is an unused port, or change it if nessessary.

This will create the directory `bteam` in `/opt/mscs/worlds` as well as the `server.properties` and `mscs.properties` files:

Change the directory to the world that was created:

    cd /opt/mscs/worlds/bteam

Rename `server.properties` to `server.properties.bak` so a back up of these settings is available

    mv server.properties server.properties.bak

These settings can be used in case `server.properties` is overwritten or deleted

    level-name=bteam
    server-port=25565
    server-ip=
    enable-query=true
    query.port=25565

[Download](http://www.technicpack.net/modpack/attack-of-the-bteam.552556) the mod pack to the world directory

    wget http://servers.technicpack.net/Technic/servers/bteam/BTeam_Server_v1.0.12c.zip

Unzip the mod pack

    unzip <current_version>.zip

While unzipping, it may ask to overwrite `server.properties`  
If you first renamed `server.properties` to `server.properties.bak` it should not ask to overwrite

Move or remove the zip

    mv <current_version>.zip /path/to/final/location/
    rm <current_version>.zip

Edit `mscs.properties` and add these settings  
If a setting below already exists in `mscs.properties`, replace it with these

    mscs-client-version=1.6.4
    mscs-initial-memory=2G
    mscs-maximum-memory=3G
    mscs-server-jar=BTeam.jar
    mscs-server-location=/opt/mscs/worlds/bteam

Merge the settings from `server.properties.bak` to the `server.properties` file created by the Technic pack.  
You should replace any setting from Technic's `server.properties` with the setting found in the backup `server.properties.bak`

    level-name=bteam
    server-port=25565
    server-ip=
    enable-query=true
    query.port=25565

Start the server

    mscs start bteam

The server should start up and run  
The server startup can be monitored by running:

    mscs console bteam

Once you are done watching the server boot up, you can press `<Ctrl-D>` to detach.
