---
layout: default
title: Crash Detection
nav_order: 7
permalink: /docs/mscs/crash-detection
---

#  Automatic Crash Detection & Restarts
{: .no_toc }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Enabling Automatic Crash Detection & Restarts

MSCS has the ability to automatically restart after a crash is detected in-game. 

This feature can be set on a global basis or on a per-world basis. By default, this feature is disabled (both globally and on a per-world basis).

Any per-world setting will override the global behavior, as detailed in [Adjusting World & Server Properties](https://minecraftservercontrol.github.io/docs/mscs/adjusting-world-server-properties). 

### Enabling it globally

To enable automatic crash detection & restarts on a global basis, set the `mscs-default-restart-after-crash` flag to `true` in your `mscs.defaults` file (see [Adjusting World & Server Properties](https://minecraftservercontrol.github.io/docs/mscs/adjusting-world-server-properties) if you're confused where to find this file).

### Enabling it on a per-world basis

To set it on a per-world basis, set the `mscs-restart-after-crash` flag to `true` in your world's `mscs.properties` file (see [Adjusting World & Server Properties](https://minecraftservercontrol.github.io/docs/mscs/adjusting-world-server-properties) if you're confused where to find this file).

--

## Notes

Please note that this feature treats in-game stop commands as crashes (so if you were to run /stop in your world with this feature enabled, it will restart).

If a world crashes and it restarts, it will notify you the next time you ran a `mscs status` command, with notes on what logs to look at to find more information. For instance:

```
$ mscs status
Minecraft Server Status:
  alex: running version 1.16.2 (0 of 20 users online).
    Port: 25567.
    Memory used: 1.04GB (2GB allocated).
    Server PID: 3351.
    Crash Monitor PID: 19569
    alex automatically restarted from a crash (or in-game stop command)
    on 2020-08-15_22-49-13. See
    /opt/mscs/worlds/alex/logs/mscs.monitor.log and
    /opt/mscs/worlds/alex/crash_reports/ and
    /opt/mscs/worlds/alex/logs/ for more information.
```


