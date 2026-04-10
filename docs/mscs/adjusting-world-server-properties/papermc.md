---
layout: default
title: PaperMC
nav_order: 4
parent: Adjusting World & Server Properties
permalink: /docs/mscs/adjusting-world-server-properties/papermc
---

# PaperMC

MSCS supports [PaperMC][papermc] with automatic updates via the PaperMC API. When configured,
`mscs update` will automatically download the latest build for your chosen Minecraft version and
build channel — no manual URL lookup required.

## Setup

Make sure the world is not running. Add the following to the world's `mscs.properties`:

```ini
mscs-server-type=papermc
```

That's it. On the next `mscs start` or `mscs update <world>`, MSCS will automatically fetch and
download the latest stable PaperMC build for the current Minecraft version.

## Properties

| Property | Default | Description |
|---|---|---|
| `mscs-server-type` | `vanilla` | Set to `papermc` to enable PaperMC auto-update |
| `mscs-server-version` | latest stable | Pin to a specific Minecraft version (e.g. `1.21.4`). Omit to always track the latest version supported by PaperMC. |
| `mscs-paper-channel` | `STABLE` | Build channel: `STABLE`, `BETA`, or `ALPHA` |

## Updating

Run `mscs update <world>` to download the latest PaperMC build for the configured version and
channel. To force a full re-download and clear the cached build information:

```bash
mscs force-update <world>
```

## Manual Override

If you need a specific build, you can bypass the auto-update system by setting `mscs-server-url`
explicitly. When this property is set, MSCS uses it directly instead of querying the PaperMC API.

```ini
mscs-server-type=papermc
mscs-server-version=1.21.4
mscs-server-jar=paper-1.21.4-116.jar
mscs-server-url=https://fill-data.papermc.io/v1/objects/abc123.../paper-1.21.4-116.jar
```

[papermc]: https://papermc.io/
