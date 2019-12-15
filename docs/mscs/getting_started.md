---
layout: default
title: Getting Started
nav_order: 3
permalink: /docs/mscs/getting_started
---

# Getting Started
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

# Creating a new world
The command to create a new world is:

    mscs create [world] [port] <ip>

Where `world` is the name of the world you specify,
and `port` is the server port (by default, use `25565`).
`ip` is optional and will be used if you wish to bind a world server to a
specific network interface (e.g. `127.0.0.1` to enforce local access only).

Afterwards, start the server via `mscs start [world]` where `world` is the
name of the world. The world will then shut down because you have to accept
the EULA.

The EULA can be found in `/opt/mscs/worlds/myWorld` where `myWorld`
is the name given to the world you created.

---

# Importing an existing world

If you wish to import or make a copy of an existing world (perhaps one that
you have not been using with mscs), simply do the following:

For this example, I change to a directory containing a world that I have
running named `alpha`, and get a directory listing:
```bash
$ ls
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

Alternatively, I could have simply provided the world's directory that sits in
my home folder instead of changing directories:

```bash
mscs import ~/minecraft_world alpha 25565
```

---

# Renaming a world
In this example we want to rename a world named `alpha` to `vanillaMC`:

```bash
mscs rename alpha vanillaMC
```bash
