---
layout: default
title: Backups
parent: Scheduling tasks
nav_order: 1
---

# Backups
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Using backup
This is the easy part. To backup:

    mscs backup <world>

Where `<world>` is the world to backup. Leaving `<world>` off will back up all worlds.

By default, backups are saved in `/opt/mscs/backups`. The location backups are saved can be configured by changing `mscs-backup-location` in `mscs.defaults` or the world's `mscs.properties` config file (See [adjusting world & server properties](https://minecraftservercontrol.github.io/docs/mscs/adjusting-world-server-properties)).

---

## Scheduling backups
Below is an example of one way you could setup backups via `cron` to backup a
world every 2 hours:

Edit the crontab file for the `minecraft` user using `sudo`:

    sudo crontab -e -u minecraft

Page down until you get to an empty line. Then paste the following:

    # Define HOME and PATH
    HOME=/opt/mscs
    PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

    # Run mscs backups
    0 */2 * * *  mscs backup myWorld

* We define HOME and PATH because `cron` may not do it for us. The HOME and PATH we've
  defined above are the default values set with the default installation.
  If you did  not follow the default installation, *Make sure that
  PATH and HOME match the environment on your system.* 

* `0 */2 * * *` is the time interval to backup. This particular expression
  means backup every 2 hours. We list some more common examples below.

* `myWorld` is the name of the world you wish to backup. Omitting this will
  backup all worlds.
  
---  
 
### Scheduling examples
Run the backup hourly.

    # Minecraft backup worlds
    0 * * * * /usr/local/bin/mscs backup

Run the backup every 2 hours.

    # Minecraft backup worlds
    0 */2 * * * /usr/local/bin/mscs backup

Run the backup every day at midnight.

    # Minecraft backup worlds
    0 0 * * * /usr/local/bin/mscs backup

---

## Viewing and restoring backups
Once you've scheduled backups, you can view the backups created by running the `mscs list-backups` command, and restore a backup using the `mscs restore-backup` command. 

You can specify how long to keep backups by changing the
`mscs-backup-duration` property in `mscs.defaults` or the world's `mscs.properties` config file (see [adjusting world & server properties](https://minecraftservercontrol.github.io/docs/mscs/adjusting-world-server-properties)).

### Example
To list the date and time of all available backups for a world named `alpha`:

    mscs list-backups alpha

To restore a specific backup for `alpha`:

    mscs restore-backup alpha 2015-03-25T21:15:11-06:00

