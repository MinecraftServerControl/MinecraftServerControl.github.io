---
layout: default
title: Updating
nav_order: 9
permalink: /docs/mscs/updating
---

# Updating
{: .no_toc }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Updating MSCS

Periodically Minecraft Server Control Script is updated to address bug fixes and add new features.

### Quick-start Installation

If you followed the [quick start installation](installation#quick-start), you can update MSCS by running the following
in the folder where you downloaded MSCS:

```bash
git pull
sudo make update
```

### Manual Installation

If you followed the [manual installation](installation#manual-installation), you will need to repeat the installation
process again to update the script.

---

## Updating Minecraft Server Version

### Vanilla server

If you are running a regular, unmodded Minecraft server (i.e. one where you didn't specify `mscs-server-jar` such a
SpigotMC or Forge), you can simply type `mscs update <world1> <world2> <...>` to update the specific world(s) to the
latest Minecraft version. Note that you can specify if you want to update to the latest Minecraft release or to the
latest Minecraft snapshot by specifying `mscs-version-type` as `release` (default) or `snapshot` in the world's
`mscs.properties`.

### Modded Server

If you are running a modded Minecraft server (i.e. one where you specified `mscs-server-jar` to something like SpigotMC
or Forge), the `mscs update` command will not work. This is because the `mscs update` command functions by looking at
the `version_manifest.json` file located in `/opt/mscs/version_manifest.json` that is downloaded from Mojang.

We recommend you follow the instructions listed for [PaperMC](adjusting-world-server-properties/papermc) to update
modded servers, or re-download the mod to the latest version if all else fails.
