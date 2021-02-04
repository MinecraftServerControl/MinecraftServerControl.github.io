---
layout: default
title: Crash Detection
nav_order: 7
permalink: /docs/mscs/crash-detection
---

## Automatic Crash Detection & Restarts

MSCS has the ability to automatically restart after a crash is detected. This feature can be set on a global basis or on a per-world basis. By default, this feature is disabled (both globally and on a per-world basis).

Any per-world setting will override the global behavior, as detailed in [Adjusting World & Server Properties](https://minecraftservercontrol.github.io/docs/mscs/adjusting-world-server-properties). 

### Globally

To enable automatic crash detection & restarts on a global basis, set the `mscs-default-restart-after-crash` flag to `true` in your `mscs.defaults` file.

### Per-world basis

To set it on a per-world basis, set the `mscs-restart-after-crash` flag to `true` in your world's `mscs.properties` file. 

