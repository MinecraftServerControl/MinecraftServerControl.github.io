---
layout: default
title: PaperMC 
nav_order: 1
parent: Adjusting World & Server Properties
permalink: /docs/mscs/adjusting-world-server-properties/papermc
---

# PaperMC

Follow the instructions below to set [PaperMC][papermc] up for a world that already exists
(see [getting started](getting-started)).

Make sure the world is not running. Then, set the server download URL in the world's `mscs.properties`:

```ini
mscs-server-url=https://papermc.io/api/v1/paper/$SERVER_VERSION/latest/download
```

Set the JAR to use in the world's `mscs.properties`:

```ini
mscs-server-jar=paperclip.jar
```

Set the server version you want in the world's `mscs.properties`. When you want  to update, you can change the version:

```ini
mscs-client-version=1.14
mscs-server-version=1.14
```

That's it! When you start the world, it should now be running PaperMC.

The PaperMC directories will be created in the world folder.

[papermc]: https://papermc.io/
