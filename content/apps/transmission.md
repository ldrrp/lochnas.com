---
title: "Transmission"
date: 2022-11-29
description: "A BitTorrent client which features a variety of user interfaces on top of a cross-platform back-end."
tags: ["apps", "docs", "transmission"]
---

## Details

This is a template to add this container to your nas setup full functional with matching permissions and settings that of lochnas repo.

Original maintainer [haugene/transmission-openvpn](https://hub.docker.com/r/haugene/transmission-openvpn/)

## How to enable

Add the domain ssl replacing domain.com with the root domain you entered in your config.yml

```
/lochnas/server.bin -domain add transmission.{domain.com}
```

Edit your `/lochnas/docker-templates/transmission/.env` file and enable this container with `TRANSMISSION_ENABLED=true` and other variables. You can access it via https://transmission.yourdomain.com/web/

The other variables are required with this vpn only transmission container.

## Custom Transmission RSS

Inside portainer you can add your own rss feeds by making a new container like so

```
 rss:
  image: haugene/transmission-rss
  links:
    - transmission
  environment:
    - RSS_URL=http://.../xxxxx.rss
```

Alternatively we recommend you look at sonarr and radarr apps for a better way to add rss feeds.