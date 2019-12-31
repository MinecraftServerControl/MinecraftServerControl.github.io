---
layout: default
title: Command reference
nav_order: 9
permalink: /docs/mscs/command-reference
---

# Command Reference
All commands below assume that you are running them as either the `minecraft`
user or as `root` (through sudo). Please note that if the script is run as the
`root` user, all important server processes will be started using the `minecraft`
user instead for security purposes.

__Usage:  `mscs [<options>] <action>`__

{: .fs-1 }
The `[<options>]` argument is optional and is not typically used. We list options
at the end of this page.

---

Actions:

```
start <world1> <world2> <...>
  Start the Minecraft world server(s).  Start all world servers by default.

stop <world1> <world2> <...>
  Stop the Minecraft world server(s).  Stop all world servers by default.

force-stop <world1> <world2> <...>
  Forcibly stop the Minecraft world server(s).  Forcibly stop all world
  servers by default.

restart <world1> <world2> <...>
  Restart the Minecraft world server(s).  Restart all world servers by default.

force-restart <world1> <world2> <...>
  Forcibly restart the Minecraft world server(s).  Forcibly restart all world
  servers by default.

create <world> <port> [<ip>]
  Create a Minecraft world server.  The world name and port must be
  provided, the IP address is usually blank.  Without arguments, create a
  a default world at the default port.

import <directory> <world> <port> [<ip>]
  Import an existing world server.  The world name and port must be
  provided, the IP address is usually blank.

rename <original world> <new world>
  Rename an existing world server.

delete <world>
  Delete a Minecraft world server.

disable <world1> <world2> <...>
  Temporarily disables world server(s). Disables all world servers by default.

enable <world1> <world2> <...>
  Enable disabled world server(s). Enables all world servers by default.

ls <option>
  Display a list of worlds.
  Options:
    enabled   Display a list of enabled worlds, default.
    disabled  Display a list of disabled worlds.
    running   Display a list of running worlds.
    stopped   Display a list of stopped worlds.
  If no option, all available worlds are listed.

list <option>
  Same as 'ls' but more detailed.

status <world1> <world2> <...>
  Display the status of Minecraft world server(s).  Display the status of
  all world servers by default.

sync <world1> <world2> <...>
  Synchronize the data stored in the mirror images of the Minecraft world
  server(s).  Synchronizes all of the world servers by default.  This option
  is only available when the mirror image option is enabled.

broadcast <command>
  Broadcast a command to all running Minecraft world servers.

send <world> <command>
  Send a command to a Minecraft world server.

console <world>
  Connect to the Minecraft world server's console.  Hit <Ctrl-D> to detach.

watch <world>
  Watch the log file for the Minecraft world server.

logrotate <world1> <world2> <...>
  Rotate the log file for the Minecraft world(s).  Rotate the log file for
  all worlds by default.

backup <world1> <world2> <...>
  Backup the Minecraft world(s).  Backup all worlds by default.

list-backups <world>
  List the datetime of the backups for the world.

restore-backup <world> <datetime>
  Restore a backup for a world that was taken at the datetime.

map <world1> <world2> <...>
  Run the Minecraft Overviewer mapping software on the Minecraft world(s).
  Map all worlds by default.

update <world1> <world2> <...>
  Update the server software for the Minecraft world server(s).  Update
  server software for all worlds by default.

force-update <world1> <world2> <...>
  Refresh version information prior to running update for the world
  server(s), regardless of how recently the version information was updated.
  Refreshes version information and updates all world servers by default.

query <world1> <world2> <...>
  Run a detailed Query on the Minecraft world server(s). Run a detailed
  query on all world servers by default.
```

Options:
```
-c <config_file>
  Read configuration from <config_files> instead of default locations.

-l <location>
  Uses <location> as the base path for data.  Overrides configuration file
  options.

```
