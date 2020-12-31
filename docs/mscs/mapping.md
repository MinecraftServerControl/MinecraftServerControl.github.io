---
layout: default
title: Mapping
nav_order: 6
permalink: /docs/mscs/mapping
---

# Mapping

{: .no_toc }

## Table of Contents

{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Setting up mapping

Overviewer is the mapping software that MSCS uses. It has pretty straightforward documentation for installation:

- [Debian / Ubuntu][building]
- [CentOS / RHEL / Fedora][install_rhel]

> __NOTE:__ For Debian / Ubuntu, we suggest [building Overviewer from source][building] instead using their apt
> repository as it is broken on the newer versions of Debian / Ubuntu (eg 20.04).

__Once you follow the install page, come back here for further instructions. Don't read the "Running the Overviewer"
section, as it will differ in MSCS.__

### Configuring Overviewer

In the `mscs.defaults` file (see [Adjusting World & Server Properties](adjusting-world-server-properties)), you'll find
various Overviewer mapping settings which you change to your liking.

We've listed the map-related settings below:

- `mscs-overviewer-bin`: This is the location for the Overviewer binary file (`overviewer.py`).
  If you manually installed Overviewer to another location, you can enter the location here.
- `mscs-overviewer-url`: A clickable link for users in chat to view the overviewer website.
- `mscs-maps-location`: The location to store the generated maps. Change this value
   to your web-server folder, e.g. `var/www/` (or symlink your web-server folder to this value).
- `mscs-maps-url`: The link to be displayed in chat to view the maps when mapping is complete.

### Changing the Default Rendering Settings

By default, we've set up MSCS to render the overworld, the Nether, the End, and cave systems with Overviewer's "normal"
render settings. However, Overviewer has many different render modes which you can apply to as many or as few dimensions
of your world(s) as you like.

All you have to do is change the config file, which is located at `/opt/mscs/worlds/myWorld/overviewer_settings.py`,
where `myWorld` is the name of your world.

To view more information on render modes and how to customize the config file, [click here][config].

---

## Mapping World(s)

After you've changed the settings, run:

```bash
mscs map <world>
```

Where `<world>` is the name of the world you would like to get mapped. Omit the world name to map all worlds.

Please note that in order for the map to update new changes in the world, you need to run Overviewer periodically.
Please see [scheduling tasks](scheduling-tasks) for more information

**Bug Note**: as of May 2020, there is a bug in Overviewer that occurs in certain system installations that have
multiple Minecraft versions located in the `/opt/mscs/.minecraft/versions` folder. In systems with this bug, the
`mscs map` command will hang and mapping will never complete (see [Issue #238][map_issue]).
If running the `mscs map` command hangs and never completes, and you have multiple versions of minecraft located in the
`/opt/mscs/.minecraft/versions` folder, please try deleting all versions except the version that you need for your world
and attempt mapping again. If you're still having issues, [please submit an issue on Github][mscs_issues].

[install_debian]: http://docs.overviewer.org/en/latest/installing/#debian-ubuntu
[install_rhel]: http://docs.overviewer.org/en/latest/installing/#centos-rhel-fedora
[download]: http://overviewer.org/downloads
[building]: http://docs.overviewer.org/en/latest/building/
[config]: http://docs.overviewer.org/en/latest/config/
[map_issue]: https://github.com/MinecraftServerControl/mscs/issues/238
[mscs_issues]: https://github.com/MinecraftServerControl/mscs/issues/
