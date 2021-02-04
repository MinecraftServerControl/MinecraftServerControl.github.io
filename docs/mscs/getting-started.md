---
layout: default
title: Getting Started
nav_order: 3
permalink: /docs/mscs/getting-started
---

# Getting Started
{: .no_toc }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Creating a New World

The command to create a new world is:

```bash
mscs create [world] [port] <ip>
```

Where `world` is the name of the world you specify, and `port` is the server port (by default, use `25565`). `ip` is
optional and will be used if you wish to bind a world server to a specific network interface (e.g. `127.0.0.1` to
enforce local access only).

Afterwards, start the server via `mscs start [world]` where `world` is the name of the world. The world will then shut
down because you have to accept the EULA. The EULA can be found in `/opt/mscs/worlds/myWorld` where `myWorld` is the
name given to the world you created. Once this is accepted, you can start the world and it will successfully load up.

Please note that, by default, the world created will be running the latest server version.
See [Adjusting World & Server Properties](adjusting-world-server-properties) for instructions on how to change this.

---

## Importing an Existing World

If you wish to import or make a copy of an existing world (perhaps one that you have not been using with mscs), simply
do the following:

For this example, change to a directory containing a world that is running named `alpha`, and get a directory listing:

```bash
ls
```

Result:

```
alpha
banned-ips.txt
banned-players.txt
crash-reports
logs
ops.txt
server.properties
white-list.txt
```

Now I simply tell mscs to create a new world from the current directory:

```bash
mscs import . alpha 25565
```

Alternatively, I could have provided the directory the `alpha` world resides in (named `minecraft_world` and located in
my Documents folder in the example below) instead of changing directories:

```bash
mscs import Documents/minecraft_world alpha 25565
```

Please note that, by default, the world created will be running the latest server version.
See [Adjusting World & Server Properties](adjusting-world-server-properties) for instructions on how to change this.

---

## Enabling/Disabling Worlds

"Enabled" worlds in MSCS are made available to MSCS commands, whereas "disabled" worlds in MSCS are not.
For instance, commands such as `mscs start` and `mscs backup` can only operate on enabled worlds.
By default, all worlds are enabled. You may wish to disable a world if you don't use it anymore and as such don't want
it included when running MSCS commands.

You can enable and disable worlds using the `mscs enable <world1> <world2> <...>`
and `mscs disable <world1> <world2> <...>` commands, respectively.

---

## Listing Worlds

MSCS has three commands to list worlds: `mscs ls`, `mscs list`, and `mscs status`.

`mscs ls` will tell you what worlds are enabled and disabled, and the ports they are running on:

```bash
mscs ls
```

Result:

```
  alex: 25567
  test: 25565
  creative: 25562 (disabled)
  forge: 25563 (disabled)
```

`mscs list` is similar to `mscs ls`, but provides more detailed info from each world's `server.properties` file:

```bash
mscs list
```

Result:

```
  alex:
    motd=A Minecraft Server    server-ip=    server-port=25567    max-players=20    level-type=default    online-mode=true

  test
    motd=A Minecraft Server    server-ip=    server-port=25569    max-players=20    level-type=default    online-mode=true
```

`mscs status`, in contrast to the above commands, runs a [query](https://wiki.vg/Query) for each world to get
information such as the player count and memory usage:

```bash
mscs status
```

Result:

```
Minecraft Server Status:
  alex: not running.
  test: running version 1.16.4 (1 of 20 users online).
    Port: 65565
    Players: Tester123.
    Memory used: 1.36GB (2GB allocated)
    Process ID: 13548.
```

`mscs status` may take a few seconds to return results because it runs a query.
Additionally, during the world's first 20-60 seconds after startup, the status will return a `world starting up` message
as it waits for the world to fully finish starting up. Please try running the status command again after a short wait if
you receive this message.

---

## Renaming a World

In this example we want to rename a world named `alpha` to `vanillaMC`:

```bash
mscs rename alpha vanillaMC
```
