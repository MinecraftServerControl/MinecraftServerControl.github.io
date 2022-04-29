---
layout: default
title: Forge
nav_order: 3
parent: Adjusting World & Server Properties
permalink: /docs/mscs/adjusting-world-server-properties/forge
---

# Forge All Versions

[Forge][forge] has an easy to use installer that can be used to install all of the needed files to run a Forge server. [Download][download] the Forge installer `forge-forge-x.x.x-x.x.x-installer` and run the following as the `minecraft` user (`sudo su minecraft`) (Note: forge for Minecraft 1.16.4 is being used as an example.):

```bash
mkdir -p /opt/mscs/server/forge-1.16.4-35.1.7
cd /opt/mscs/server/forge-1.16.4-35.1.7
wget https://files.minecraftforge.net/maven/net/minecraftforge/forge/1.16.4-35.1.7/forge-1.16.4-35.1.7-installer.jar
java -jar forge-1.16.4-35.1.7-installer.jar --installServer
```
The next steps are divided between _Forge 1.16.5 and before_ and _Forge 1.17.1 and later_. This is because the way that forge-1.17.1 was structered changed because ["it is no longer feasible to provide a single executable jar like was done before."][forge-1.17.1_release_notes]

## Forge 1.16.5 and before
Please note that forge for Minecraft 1.16.4 will be used in the examples. The installer should install the forge server jar to `/opt/mscs/server/forge-1.16.4-35.1.7/forge-1.16.4-35.1.7.jar`
and a bunch of library files in `/opt/mscs/server/forge-1.16.4-35.1.7/libraries/`.

Create a new server (if necessary):

```bash
mscs create forge 25565
```

`forge` can be replaced with any name. Ensure that port `25565` is an unused port, or change it if nessessary.

This will create the directory `forge` in `/opt/mscs/worlds` as well as the `server.properties` and `mscs.properties`
files:

Change the directory to the world that was created:

```bash
cd /opt/mscs/worlds/forge
```

Modify the `mscs.properties` file and add/alter these lines, replacing versions and file paths as needed:

```bash
editor /opt/mscs/worlds/forge/mscs.properties
```

Add this

```ini
mscs-client-version=1.16.4
mscs-server-version=1.16.4
mscs-server-jar=forge-1.16.4-35.1.7/forge-1.16.4-35.1.7.jar
mscs-server-url=
```

You may also want to increase the initial RAM and possibly even the maximum RAM.

> Minimum default is 128M  
> Maximum default is 2048M

```ini
mscs-initial-memory=1024M
mscs-maximum-memory=3048M
```

If the server fails to start, the `eula.txt` file may need to be edited and accepted:

```bash
editor /opt/mscs/worlds/forge/eula.txt
```

Change `false` to `true`

```ini
eula=true
```

Stop then Start the server:

```bash
mscs stop forge
mscs start forge
```

The server should start up and run

The server startup can be monitored by running:

```bash
mscs watch forge
```

Once you are done watching the server boot up, you can press `<Ctrl-C>` to detach.

Simply add mods as you would normally by dragging them into the `/opt/mscs/worlds/forge/mods` folder, assuming `forge`
is the name of your world.


## Forge 1.17.1 and later
Please note that forge for Minecraft 1.17.1 will be used in the examples. If you named the server directory `forge-1.17.1` in the first step with the `mkdir` command, the installer should install a bash script to `/opt/mscs/server/forge-1.17.1` and a bunch of library files in `/opt/mscs/server/forge-1.17.1/libraries/`.

There's an automatic and a manual way to apply the fixes needed for these versions. 

### Automatic

**In the `/opt/mscs/server/forge-1.17.1` directory**, execute these commands: 

```bash
sed -i "\|@[^\"]|s|@|@$(pwd)/|" run.sh
sed -i "s|\"\$@|--nogui &|g" run.sh
sed -i "s|libraries|$(pwd)/libraries|g" libraries/net/minecraftforge/forge/*/unix_args.txt
```

<details>
<summary>Explanation of the sed commands</summary>


<span markdown='span'>`sed -i "\|@[^\"]|s|@|@$(pwd)/|" run.sh`: This matches all occurences of `@` that aren't followed by `"` and adds the current directory followed by a / to it (or rather, replaces the `@` with an `@` followed by the current directory).</span> <br>

<span markdown='span'>`sed -i "s|\"\$@|--nogui &|g" run.sh`: This adds `--nogui ` in front of `"$@`, with `&` being the matched pattern.</span><br>

<span markdown='span'>`sed -i "s|libraries|$(pwd)/libraries|g" libraries/net/minecraftforge/forge/*/unix_args.txt`: This adds the current path to all occurences of the word libraries in the unix_args.txt file. Because the directory contains the forge version (for example `1.17.1-37.1.1`), `*` is used as a wildcard.</span>

</details>
<br>
Continue below at <a href="#end-manual"><strong>You may also want...</strong></a>

### Manual

In the `/opt/mscs/server/forge-1.17.1` directory, edit `run.sh`. 

(GNU nano is an easy to use command-line text editor if you plan to edit the file from the terminal. Install it with `sudo apt install nano` if you are using a Debian based distro. In the following instructions, to edit a file with GNU nano, replace `editor` with `nano`.)

```bash
cd /opt/mscs/server/forge-1.17.1
editor run.sh
```

The original `run.sh` script wil include `java @user_jvm_args.txt @libraries/net/minecraftforge/forge/1.17.1-37.1.1/unix_args.txt "$@"`

The `@user_jvm_args.txt` and the `@libraries/net/minecraftforge/forge/1.17.1-37.1.1/unix_args.txt` need to be replaced with their full directory path. You should also include `--nogui` at the end **of the same line** before the `"$@"`. The file should now look like this:

```ini
#!/usr/bin/env sh
# Forge requires a configured set of both JVM and program arguments.
# Add custom JVM arguments to the user_jvm_args.txt
# Add custom program arguments {such as nogui} to this file in the next line before the "$@" or
#  pass them to this script directly
java @/opt/mscs/server/forge-1.17.1/user_jvm_args.txt @/opt/mscs/server/forge-1.17.1/libraries/net/minecraftforge/forge/1.17.1-37.1.1/unix_args.txt --nogui "$@"
```

Now the `unix_args.txt` file mentioned in `run.sh` needs to be edited as well to include the full directory paths. Change the directory to the one containing the `unix_args.txt` file, create a backup in case you mess up the editing, and then edit the original.

```bash
cd /opt/mscs/server/forge-1.17.1/libraries/net/minecraftforge/forge/1.17.1-37.1.1/
cp unix_args.txt unix_args_backup.txt
editor unix_args.txt
```

Every path that includes `libraries/[...]` has to be replaced with their full directory path: `/opt/mscs/server/forge-1.17.1/libraries/[...]`. If your editor of choice is GNU nano, this can be done by pressing `<Ctrl-\>`, typing `libraries` and pressing enter, then typing the full path name. In this case it would be `/opt/mscs/server/forge-1.17.1/libraries`, then press enter, then press `<a>` to replace all. 

If you mess this up, you can always delete the `unix_args.txt` file and make another one using the backup, and start editing again.

```bash
rm unix_args.txt
cp unix_args_backup.txt unix_args.txt
editor unix_args.txt
```
<a id="end-manual"></a>

You may also want to increase the initial RAM and possibly even the maximum RAM. To do this, edit the `user_jvm_args.txt` file.

```bash
cd /opt/mscs/server/forge-1.17.1/
editor user_jvm_args.txt
```

Now add all the java arguments you wish. For example, to allocate a minimum of 4GB and a maximum of 6GB, you would make the `user_jvm_args.txt` file look something like this:

```ini
# Xmx and Xms set the maximum and minimum RAM usage, respectively.
# They can take any number, followed by an M or a G.
# M means Megabyte, G means Gigabyte.
# For example, to set the maximum to 3GB: -Xmx3G
# To set the minimum to 2.5GB: -Xms2500M

# A good default for a modded server is 4GB.
# Uncomment the next line to set it.
-Xms4G -Xmx6G
```

Create a new server (if necessary):

```bash
mscs create forge 25565
```

`forge` can be replaced with any name. Ensure that port `25565` is an unused port, or change it if nessessary.

This will create the directory `forge` in `/opt/mscs/worlds` as well as the `server.properties` and `mscs.properties`
files:

Change the directory to the world that was created and modify the `mscs.properties` file.

```bash
cd /opt/mscs/worlds/forge
editor /opt/mscs/worlds/forge/mscs.properties
```

Add/alter these lines, replacing versions and file paths as needed:


```ini
mscs-client-version=1.17.1
mscs-server-version=1.17.1
mscs-server-command=/opt/mscs/server/forge-1.17.1/run.sh
mscs-server-url=
```

If the server fails to start, the `eula.txt` file may need to be edited and accepted:

```bash
editor /opt/mscs/worlds/forge/eula.txt
```

Change `false` to `true`

```ini
eula=true
```

Stop then Start the server:

```bash
mscs stop forge
mscs start forge
```

The server should start up and run.

The server startup can be monitored by running:

```bash
mscs watch forge
```

Once you are done watching the server boot up, you can press `<Ctrl-C>` to detach.

Simply add mods as you would normally by dragging them into the `/opt/mscs/worlds/forge/mods` folder, assuming `forge`
is the name of your world.

[forge]: http://www.minecraftforge.net
[download]: http://files.minecraftforge.net
[forge-1.17.1_release_notes]: https://forums.minecraftforge.net/topic/102544-forge-370-minecraft-1171/
