---
title: "Sonarr"
date: 2022-11-29
description: "An internet PVR for Usenet and Torrents."
tags: ["apps", "docs", "sonarr", "tv"]
---

## Details

This is a template to add this container to your nas setup full functional with matching permissions and settings that of lochnas repo. This assumes you are using plex and transmission paths.

## How to enable

Add the domain ssl replacing domain.com with the root domain you entered in your config.yml

```
/lochnas/server.bin -domain add sonarr.{domain.com}
```

Edit your `/lochnas/docker-templates/sonarr/.env` file and enable this container with `SONARR_ENABLED=true` and other variables. You can access it via https://sonarr.yourdomain.com

To use web access you must have nginx auth password set

## Additional Configuration

### Enable root folder

Settings -> Media Management -> Root Folders -> Add Root Folder -> /lochnas/home/path/to/TV

### Enable Download clients

Settings -> Download Clients -> Add + -> Transmission

 - Name: `Transmission`
 - Enable: `Checked`
 - Host: `transmission.domain.com`
 - Port: `443`
 - Use SSL: `Checked`
 - Username: `<transmission username>`
 - Password: `<transmission password>`
 - Category: `sonarr`

Click test, then Save

### Enable Indexers

Settings -> Indexers -> Add +

Select the indexer your want to enable and configure