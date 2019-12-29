---
layout: default
title: BungeeCord
nav_order: 5
parent: Adjusting world & server properties
permalink: /docs/mscs/adjusting-world-server-properties/bungeecord
---

## BungeeCord
[BungeeCord] is a proxy server that sits between the Minecraft client and server that allows players on a server to easily transfer between worlds (regardless of whether the world is running on vanilla, Forge, SpigotMC, etc). The setup for BungeeCord can be rather complex. To fully understand the configuration options available, visit the [BungeeCord Configuration Guide].

Although BungeeCord is not a normal Minecraft server, [MSCS] is able to control the server as if it were with a little work. Lets start by creating a fake world named `lobby` on the default port of `25565`.

    mscs create lobby 25565

`lobby` can be replaced with any name. Ensure that port `25565` is an unused port, or change it if nessessary.

Change the directory to the world that was created:

    cd /opt/mscs/worlds/lobby

This will create the directory `lobby` in `/opt/mscs/worlds` as well as the `server.properties` and `mscs.properties` files:

`server.properties` is not needed for this server. Delete this file.

    rm server.properties

Modify the `mscs.properties` file and add/alter these lines:

    mscs-enabled=true
    mscs-server-jar=BungeeCord.jar
    mscs-server-url=
    mscs-initial-memory=512M
    mscs-maximum-memory=512M

Create a `config.yml` file that will apply for the worlds on this server. For example: `alpha` and `beta` on ports `25566` and `25567` respectively. Note, change the name of the admin from `username` to the Minecraft player name that will be administering BungeeCord.

```
groups:
  username:
  - admin
disabled_commands:
- disabledcommandhere
player_limit: -1
permissions:
  default:
  - bungeecord.command.server
  - bungeecord.command.list
  admin:
  - bungeecord.command.alert
  - bungeecord.command.end
  - bungeecord.command.ip
  - bungeecord.command.reload
listeners:
- max_players: 20
  fallback_server: alpha
  host: 0.0.0.0:25565
  bind_local_address: true
  ping_passthrough: false
  tab_list: GLOBAL_PING
  default_server: alpha
  tab_size: 20
  force_default_server: false
  motd: 'Message of the day'
  query_enabled: true
  query_port: 25565
timeout: 30000
connection_throttle: 4000
servers:
  alpha:
    address: localhost:25566
    restricted: false
    motd: '&1Alpha MOTD'
  beta:
    address: localhost:25567
    restricted: false
    motd: '&2Beta MOTD'
ip_forward: false
online_mode: true
```

Change to the `/opt/mscs/server/` directory, [download][download bungee] the BungeeCord server jar `BungeeCord.jar`, and run the following as the `minecraft` user (`sudo su minecraft`):

    cd /opt/mscs/server
    wget http://ci.md-5.net/job/BungeeCord/lastSuccessfulBuild/artifact/bootstrap/target/BungeeCord.jar

Create the two worlds `alpha` and `beta`. Since both worlds will only be accessed locally by the BungeeCord proxy server, use the optional `ip` argument for the `create` function to limit access to localhost:

    mscs create alpha 25566 127.0.0.1
    mscs create beta 25567 127.0.0.1

Start the worlds to set themselves up:

    mscs start alpha
    mscs start beta

If the servers fail to start, the `eula.txt` file may need to be edited and accepted:

    editor /opt/mscs/worlds/alpha/eula.txt
    editor /opt/mscs/worlds/beta/eula.txt

BungeeCord requires that the world servers be in offline mode. BungeeCord handles authentication as long as `online_mode` is set to `true` in `config.yml` like the example above. To do this, edit the `server.properties` file for the `alpha` and `beta` worlds and change the values of `online-mode` in both files to `false`.

    editor /opt/mscs/worlds/alpha/server.properties
    editor /opt/mscs/worlds/beta/server.properties

Finally, if everything is correctly setup, we can start the worlds:

    mscs start lobby
    mscs start alpha
    mscs start beta
