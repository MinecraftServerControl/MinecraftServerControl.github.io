---
layout: default
title: Updating
nav_order: 8
permalink: /docs/mscs/updating
---

# Updating
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Updating MSCS

### Quick-start installation
Periodically Minecraft Server Control Script is updated to address bug fixes and add new features. If you followed the [quick start installation](https://minecraftservercontrol.github.io/docs/mscs/installation#quick-start), you can update MSCS by `cd`'ing into the folder where you downloaded MSCS. Then, type:

```bash
git pull
sudo make update
```

### Manual installation
If you followed the [manual installation](https://minecraftservercontrol.github.io/docs/mscs/installation#manual-installation), you will need to repeat the installation process again to update the script.

---

## Updating Minecraft server version

### Vanilla server
If you are running a regular, unmodded Minecraft server (i.e. one where you didn't specify `mscs-server-jar` such a SpigotMC or Forge), you can simply type `mscs update <world1> <world2> <...>` to update the specific world(s) to the latest Minecraft version. Note that you can specify if you want to update to the latest Minecraft release or to the latest Minecraft snapshot by specifying `mscs-version-type` as `release` (default) or `snapshot` in the world's `mscs.properties`.

### Modded server
If you are running a modded Minecraft server (i.e. one where you specified `mscs-server-jar` to something like SpigotMC or Forge), the `mscs update` command will not work. This is because the `mscs update` command functions by looking at the `version_manifest.json` file located in `/opt/mscs/version_manifest.json` that is downloaded from Mojang. 

We recommend you follow the instructions listed for [PaperMC](https://minecraftservercontrol.github.io/docs/mscs/adjusting-world-server-properties/papermc) to update modded servers, or re-download the mod to the latest version if all else fails.
 
 
