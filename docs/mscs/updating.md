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

### PaperMC

If you are running a PaperMC world with `mscs-server-type=papermc`, you can use `mscs update <world>` just like a
vanilla server. MSCS will automatically fetch and download the latest build from the PaperMC API. See the
[PaperMC guide](adjusting-world-server-properties/papermc) for setup details.

### Other Modded Servers

If you are running another modded server (e.g. Forge, SpigotMC, Fabric) where you have manually set `mscs-server-jar`,
the `mscs update` command will not work. You will need to download the updated server JAR manually and update the
relevant properties in `mscs.properties`.
