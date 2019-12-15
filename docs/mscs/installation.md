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

<details>
  <summary>Collapsed Block
</summary>

  <h2 id="header">Header</h2>
</details>

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


## Quick start 

The fastest way to install the script is to clone the git repository and run the included Makefile:
```bash
git clone https://github.com/MinecraftServerControl/mscs.git && cd mscs
sudo make install
```
This will, by default, create a user to perform MSCS tasks 
called `minecraft`and give it access to write in the `/opt/mscs` folder.

## Other ways to install
