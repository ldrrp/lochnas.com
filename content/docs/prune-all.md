---
title: "Prune all images"
date: 2022-11-30
description: "How to prune all docker images"
tags: ["docker", "prune" "troubleshooting"]
---

Sometimes an app has an update and the old image retains remnants of files it should no longer have. If you find yourself having an issue that no one else can replicate you can try prunning your images and restarting lochnas so that the images rebuild. This will have no effect on your persistent data.

```bash
service lochnas stop
docker rm -f $(docker ps -a -q)
docker image prune -f
docker network prune -f
docker volume prune -f
service lochnas start
```