---
layout: default
title: Scheduling tasks
nav_order: 7
permalink: /docs/mscs/scheduling-tasks
---

# Scheduling tasks
{: .no_toc }

Schedule automatic backups, restarts, mapping and more 
using MSCS and cron, a scheduler software built into linux
that can run programs on a set interval of time. 
Any MSCS command can be scheduled using cron. We list 
instructions for the most popular commands below.
{: .fs-6 .fw-300 }

Below is an example of one way you could setup backups via `cron` to backup a
world every 2 hours:

Edit the crontab file for the `minecraft` user using `sudo`:

```bash
sudo crontab -e -u minecraft
```

Page down until you get to an empty line. Then paste the following:

```bash
# Define HOME and PATH
HOME=/opt/mscs
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# Run mscs backups
0 */2 * * *  mscs backup myWorld
```

* We define HOME and PATH because `cron` may not do it for us. The HOME and PATH we've
  defined above are the default values set with the default installation.
  If you did  not follow the default installation, *Make sure that
  PATH and HOME match the environment on your system.* 

* `0 */2 * * *` is the time interval to backup. This particular expression
  means backup every 2 hours. We list some more common examples below.

* `myWorld` is the name of the world you wish to backup. Omitting this will
  backup all worlds.
 
 ---
 
## Scheduling examples

Run the backup hourly.

```bash
# Minecraft backup worlds every hour
0 * * * * /usr/local/bin/mscs backup
```

Run the backup every 2 hours.

```bash
# Minecraft backup worlds every 2 hours
0 */2 * * * /usr/local/bin/mscs backup
```

Run the backup every day at midnight.

```bash
# Minecraft backup worlds every day at midnight
0 0 * * * /usr/local/bin/mscs backup
```

Visit [crontab.guru](http://crontab.guru) for more help on scheduling cron jobs.
