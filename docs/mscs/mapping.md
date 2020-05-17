---
layout: default
title: Mapping
nav_order: 6
permalink: /docs/mscs/mapping
---

# Mapping
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Setting up mapping
Overviewer is the mapping software that MSCS uses. 
It has pretty straightforward documentation to download and install the software:

* [Debian/Ubuntu](http://overviewer.org/debian/info)
* [RHEL/CentOS/Fedora](http://overviewer.org/rpms/info)

You can also [download](http://overviewer.org/downloads) premade binaries for
supported systems, or build your own binary from source if needed.

__Once you follow the install page, come back here for further instructions.
Don't read the "Running the Overviewer" section, as it will differ in MSCS.__

### Configuring Overviewer
In the `mscs.defaults` file 
(see [adjusting world & server properties](https://minecraftservercontrol.github.io/docs/mscs/adjusting-world-server-properties)), 
you'll find various Overviewer mapping settings which you change to your liking.
We've listed the map-related settings below:
    
* `mscs-overviewer-bin`: This is the location for the Overviewer binary.                                                               If you manually installed Overviewer to another location, you can enter the location here.
* `mscs-overviewer-url`: A clickable link for users in chat to view the overviewer website.
* `mscs-maps-location`: The location to store the generated maps. Change this value
   to your web-server folder, e.g. `var/www/` (or symlink your web-server folder to this value).
* `mscs-maps-url`: The link to be displayed in chat to view the maps when mapping is complete. 


### Changing the default rendering settings
By default, we've set up MSCS to render the overworld, the nether, the end, and cave systems 
with Overviewer's "normal" render settings. However, Overviewer has many different render 
modes which you can apply to as many or as few dimensions of your world(s) as you like.

All you have to do is change the config file, which is located at 
`/opt/mscs/worlds/myWorld/overviewer_settings.py`, where `myWorld` is the name of your world.

To view more information on render modes and how to customize the config file, 
[click here](http://docs.overviewer.org/en/latest/config/#examples).

---

## Mapping world(s)
After you've changed the settings, run:

    mscs map <world>

Where `<world>` is the name of the world you would like to get mapped.
Omit the world name to map all worlds.

Please note that in order for the map to update new changes in the world,
you need to run Overviewer periodically.
Please see [scheduling tasks](https://minecraftservercontrol.github.io/docs/mscs/scheduling-tasks) for more information

**Bug Note**: as of May 2020, there is a bug in Overviewer that occurs in certain system installations that have multiple Minecraft versions located in the `/opt/mscs/.minecraft/versions` folder. In systems with this bug, the `mscs map` command will hang and mapping will never complete ([see Issue #238](https://github.com/MinecraftServerControl/mscs/issues/238)). If running the `mscs map` command hangs and never completes, and you have multiple versions of minecraft located in the `/opt/mscs/.minecraft/versions` folder, please try deleting all versions except the version that you need for your world and attempt mapping again. If you're still having issues, [please submit an issue on Github](https://github.com/MinecraftServerControl/mscs/issues/).
