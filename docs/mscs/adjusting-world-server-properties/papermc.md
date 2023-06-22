---
layout: default
title: PaperMC 
nav_order: 4
parent: Adjusting World & Server Properties
permalink: /docs/mscs/adjusting-world-server-properties/papermc
---

# PaperMC

Follow the instructions below to set [PaperMC][papermc] up for a world that already exists
(see [getting started](getting-started)).

Make sure the world is not running. Find the URL for the version and build number for PaperMC that you wish to run from [their site][papermc]. Then, set the server download URL in the world's `mscs.properties`:

```ini
mscs-server-url=https://papermc.io/api/v2/projects/paper/versions/1.16.5/builds/438/downloads/paper-1.16.5-438.jar
```

Set the JAR to use in the world's `mscs.properties`:

```ini
mscs-server-jar=paper-1.16.5.jar
```

Set the server version you want in the world's `mscs.properties`. When you want  to update, you can change the version:

```ini
mscs-client-version=1.16.5
mscs-server-version=1.16.5
```

That's it! When you start the world, it should now be running PaperMC.

The PaperMC directories will be created in the world folder.

Note: You will need to change these same values whenever you want to upgrade to the latest version. PaperMC is unfortunately no longer providing a stable link to the latest version of their software, so you will need to modify these values by hand.

[papermc]: https://papermc.io/
