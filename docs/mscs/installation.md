---
layout: default
title: Installation
nav_order: 2
permalink: /docs/mscs/installation
---

# Installation
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Dependencies
We've made an attempt to utilize only features that are normally installed in
most Linux and UNIX environments in this script. However, there may be a few
requirements that this script has that may not already be in place:


* Java JRE                   - The Minecraft server software requires this. 
                               **As of Minecraft 1.12, Java 8 is required.**
* Perl                       - Most, if not all, Unix and Linux like systems
                               have this preinstalled.
* libjson-perl               - Allows the script to read JSON formatted data.
* libwww-perl                - Allows the script to download data to verify
                               downloads.
* liblwp-protocol-https-perl - Allows the script to download data over HTTPS.
* Python                     - Required by the Minecraft Overviewer mapping
                               software.
* GNU Make                   - Allows you to use the Makefile to simplify
                               installation.
* GNU Wget                   - Allows the script to download software updates
                               via the internet.
* rdiff-backup               - Allows the script to efficiently run backups.
* rsync                      - Allows the script to efficiently make copies of
                               files.
* Socat                      - Allows the script to communicate with the
                               Minecraft server.
* Iptables                   - Although not explicitly required, a good
                               firewall should be installed.
</small>

If you are running Debian or Ubuntu, you can make sure that these are
installed by running:
```bash
sudo apt-get install default-jre perl libjson-perl libwww-perl liblwp-protocol-https-perl python make wget git rdiff-backup rsync socat iptables
```
If you are running Fedora, you can make sure that these are
installed by running:
```bash
yum install java-1.8.0-openjdk perl perl-JSON perl-libwww-perl perl-LWP-Protocol-https python make wget git rdiff-backup rsync socat iptables sudo procps which
```

### Configuring the firewall / NAT
If you are going to run the Minecraft server on your computer, you may need to route some ports to the server (if you are running the Minecraft server with a hosting company, they most likely already have the ports open). Instructions on how to accomplish this are beyond the scope of this document, but here are some things you will need to know:

* The default port for the Minecraft server is: 25565.
* If you wish to run multiple world servers using this script, you may want to open a range of ports (for example 25565 - 25575).
* If you are using BungeeCord, you will most likely need to only open the default port: 25565.

See the [iptables.rules](https://github.com/MinecraftServerControl/mscs/blob/master/iptables.rules) file for a very basic set of rules that you can use with the Iptables firewall.

---

## Quick start 
Recommended
{: .label }

The fastest way to install the script is to clone the git repository and run the included Makefile:
```bash
git clone https://github.com/MinecraftServerControl/mscs.git && cd mscs
sudo make install
```
This will, by default, create a user to perform MSCS tasks 
called `minecraft` and give it access to write in the `/opt/mscs` folder.
If there are no errors, then you can proceed to use the script. 

[Getting started](https://minecraftservercontrol.github.io/docs/mscs/getting-started){: .btn .btn-purple }

If you get a `permission denied` error, please see the [troubleshooting](https://minecraftservercontrol.github.io/docs/mscs/troubleshooting-issues) page.

---

## Manual installation
If the instructions above do not work (i.e. fails on `sudo make install`) or if the installation requires custom locations, user accounts, or settings, then follow the instructions below.

To get a server to run the MSCS script on startup, and cleanly stop the server on shutdown, the [MSCS](https://github.com/MinecraftServerControl/mscs/blob/master/mscs) script must be copied to `/usr/local/bin/`, have execute permissions set, and the system must run the script on startup and shutdown. For Bash completion support, the `mscs.completion` script must be copied to `/etc/bash_completion.d/`. For security reasons, the script runs with an account named `minecraft` rather than `root`. The `minecraft` account must be created before the script is used.

1. Create the `minecraft` user:
```bash
useradd --system --user-group --create-home -K UMASK=0022 --home /opt/mscs minecraft
```

2. Install the script:
```bash
sudo install -m 0755 msctl /usr/local/bin/msctl
sudo install -m 0755 mscs /usr/local/bin/mscs
```

3. If using systemd (ie. Ubuntu 15.04+), link the script to the server's startup and shutdown sequences:
```bash
sudo install -m 0644 mscs.service /etc/systemd/system/mscs.service
sudo systemctl -f enable mscs.service
```

4. If using SysV-style, upstart, or similar (ie. Ubuntu 14.10 and lower) link the script to your server's startup and shutdown   sequences:
```bash
sudo ln -s /usr/local/bin/mscs /etc/init.d/mscs
sudo update-rc.d mscs defaults
```

5. Add Bash Completion support:
```bash
sudo install -m 0644 mscs.completion /etc/bash_completion.d/mscs
```

The Minecraft server software will be automatically downloaded to the following location on the first run:
```bash
/opt/mscs/server/
```

---

## Multi-user setup
MSCS has the ability to store server and world data on a user-by-user basis, allowing multiple users to run their respective worlds while preserving the data of other user worlds.

> Example: Two user accounts are available on a server: `bob` and `jason`.  
  `bob` should only be able to run and modify Bob's worlds.  
  `jason` should only be able to run and modify Jason's worlds.  
  Each user can have their own properties and world locations

To accomplish this, direct users to use `msctl` in place of `mscs` when running commands (see [command reference](https://minecraftservercontrol.github.io/docs/mscs/command-reference)). That's it!

For instance, to create a world named `world`:

    msctl create world 25565

To start `world`:

    msctl start world

For all commands, replace the `mscs` prefix with `msctl`.

By default, the location of each users' worlds will be saved to `$HOME/mscs/worlds`, where `$HOME` is the home directory of the user. So if `bob` is logged in, and Bob's home directory is `/home/bob`, Bob's worlds will be saved to `/home/bob/mscs/worlds`.

**Please note: MSCS currently does not check if a server port is free for use when creating or running worlds. All users will need to coordinate which ports are being used so no conflicts occur.**
