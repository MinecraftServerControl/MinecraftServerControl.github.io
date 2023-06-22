---
layout: default
title: Purpur
nav_order: 5
parent: Adjusting World & Server Properties
permalink: /docs/mscs/adjusting-world-server-properties/purpur
---

# Purpur

Follow the instructions below to set [Purpur][purpur] up for a world that already exists
(see [getting started](getting-started)).

Make sure the world is not running. Then, set the server download URL in the world's `mscs.properties`:

```ini
mscs-server-url=https://api.purpurmc.org/v2/purpur/$SERVER_VERSION/latest/download
```

Set the JAR to use in the world's `mscs.properties`:

```ini
mscs-server-jar=purpurclip.jar
```

Set the server version you want in the world's `mscs.properties`. When you want to update, you can change the version:

```ini
mscs-client-version=1.16.5
mscs-server-version=1.16.5
```

That's it! When you start the world, it should now be running Purpur.

The Purpur directories will be created in the world folder.

[purpur]: https://purpurmc.org/
