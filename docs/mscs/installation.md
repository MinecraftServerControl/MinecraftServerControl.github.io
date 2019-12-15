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
---

## Quick Start 

The fastest way to install the script is to clone the git repository and run the included Makefile:
```bash
git clone https://github.com/MinecraftServerControl/mscs.git && cd mscs
sudo make install
```
This will, by default, create a user to perform MSCS tasks 
called `minecraft`and give it access to write in the `/opt/mscs` folder.

---

## Manual Installation
Follow the instructions below if the installer does not work (`sudo make install`) or if the installation requires custom locations, user accounts, or settings.

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
3a. If using systemd (ie. Ubuntu 15.04+), link the script to the server's startup and shutdown sequences:
```bash
sudo install -m 0644 mscs.service /etc/systemd/system/mscs.service
sudo systemctl -f enable mscs.service
```
3b. If using SysV-style, upstart, or similar (ie. Ubuntu 14.10 and lower) link the script to your server's startup and shutdown   sequences:
  ```bash
  sudo ln -s /usr/local/bin/mscs /etc/init.d/mscs
  sudo update-rc.d mscs defaults
```
4. Add Bash Completion support:
```bash
sudo install -m 0644 mscs.completion /etc/bash_completion.d/mscs
```
The Minecraft server software will be automatically downloaded to the following location on the first run:
```bash
/opt/mscs/server/
```
