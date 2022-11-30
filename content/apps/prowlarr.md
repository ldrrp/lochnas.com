---
title: "Prowlarr"
date: 2022-11-29
description: "An indexer manager/proxy built on the popular arr .net/reactjs base stack to integrate with your various PVR apps"
tags: ["apps", "docs", "prowlarr"]
---

## Details

This is a template to add this container to your nas setup full functional with matching permissions and settings that of lochnas repo. This assumes you are using plex and transmission paths.

## How to enable

Add the domain ssl replacing domain.com with the root domain you entered in your config.yml

```
/lochnas/server.bin -domain add prowlarr.{domain.com}
```

Edit your `/lochnas/docker-templates/prowlarr/.env` file and enable this container with `PROWLARR_ENABLED=true` and other variables. You can access it via https://prowlarr.yourdomain.com

To use web access you must have nginx auth password set

## Enable Download clients

Settings -> Download Clients -> Add + -> Transmission

 - Name: `Transmission`
 - Enable: `Checked`
 - Host: `transmission.domain.com`
 - Port: `443`
 - Use SSL: `Checked`
 - Username: `<transmission username>`
 - Password: `<transmission password>`
 - Category: `prowlarr`

Click test, then Save

## Enable Indexers

Indexers -> Add New Indexer

Select the indexer your want to enable and configure
