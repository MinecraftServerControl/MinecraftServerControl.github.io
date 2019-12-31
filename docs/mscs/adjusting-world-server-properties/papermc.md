---
layout: default
title: PaperMC 
nav_order: 1
parent: Adjusting world & server properties
permalink: /docs/mscs/adjusting-world-server-properties/papermc
---

# PaperMC

Follow the instructions below to set [PaperMC](https://papermc.io/)
up for a world that already exists (see [getting started](https://minecraftservercontrol.github.io/docs/mscs/getting-started)).

Make sure the world is not running. 
Then, set the server download URL in the world's `mscs.properties`:

```
mscs-server-url=https://papermc.io/ci/job/Paper-$SERVER_VERSION/lastSuccessfulBuild/artifact/paperclip.jar
```

Set the JAR to use in the world's `mscs.properties`:

```
mscs-server-jar=paperclip.jar
```

Set the server version you want in the world's `mscs.properties`. When you want 
to update, you can change the version:

```
mscs-client-version=1.14
mscs-server-version=1.14
```

That's it! When you start the world, it should now be running PaperMC.
The PaperMC directories will be created in the world folder. 

