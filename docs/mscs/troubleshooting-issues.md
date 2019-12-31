---
layout: default
title: Troubleshooting/issues
nav_order: 9
permalink: /docs/mscs/troubleshooting-issues
---

# Troubleshooting

If you get a `permission denied` error when attempting to
run a `mscs` command, please ensure that the `minecraft`
user has the correct permissions set:

chmod -R u+w /opt/mscs
chown -R minecraft:minecraft /opt/mscs

# Issues

We have only tested this code in a Debian/Ubuntu environment, but there is no reason that it shouldn't work in any appropriately configured UNIX-like environment, including Apple Mac OSX and the other BSD variants, with only minor modifications. If you experience errors running this script, please post a copy of the error message and a note detailing the operating environment where the error occurs to the support thread, and we will try to work out a solution with you

For a list of current and past issues, or to submit an issue or question you have,
please visit the [Github issues page](https://github.com/MinecraftServerControl/mscs/issues).
