---
title: "Readarr"
date: 2022-11-29
description: "Readarr is an ebook and audiobook collection manager for Usenet and BitTorrent"
tags: ["apps", "docs", "readarr", "ebooks", "audiobooks"]
---

## Details

This is a template to add this container to your nas setup full functional with matching permissions and settings that of lochnas repo. This assumes you are using plex and transmission paths.

## How to enable

Add the domain ssl replacing domain.com with the root domain you entered in your config.yml

```
/lochnas/server.bin -domain add readarr.{domain.com}
```

Edit your `/lochnas/docker-templates/readarr/.env` file and enable this container with `READARR_ENABLED=true` and other variables. You can access it via https://readarr.yourdomain.com

To use web access you must have nginx auth password set

## Additional Configuration

### Enable root folder

Settings -> Media Management -> Root Folders -> Add Root Folder -> /lochnas/home/path/to/Books

### Enable Download clients

Settings -> Download Clients -> Add + -> Transmission

 - Name: `Transmission`
 - Enable: `Checked`
 - Host: `transmission.domain.com`
 - Port: `443`
 - Use SSL: `Checked`
 - Username: `<transmission username>`
 - Password: `<transmission password>`
 - Category: `readarr`

Click test, then Save

### Enable Indexers

Settings -> Indexers -> Add +

Select the indexer your want to enable and configure