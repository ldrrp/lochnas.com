---
title: "Shinobi"
date: 2022-12-16
description: "Network video recorder"
tags: ["apps", "docs", "shinobi"]
---

## Details

This template adds Shinobi, a network video recorder (NVR) for viewing and recording IP cameras.

Original maintainer [MiGoller's ShinobiDocker](https://hub.docker.com/r/migoller/shinobidocker), [mariadb](https://hub.docker.com/_/mariadb)

## How to enable

Add the domain to get SSL, replacing "domain.com" with the root domain (configured in config.yml)

```
/lochnas/server.bin -domain add shinobi.{domain.com}
```

Copy `/lochnas/docker-templates/shinobi/.example.env` to `/lochnas/docker-templates/shinobi/.env`. Edit `/lochnas/docker-templates/shinobi/.env`

Set `SHINOBI_ENABLED=TRUE`. Fill in the passwords with random and keep note of ADMIN_USER and ADMIN_PASSWORD. These values will be set on initial setup.

an example .env:
```
SHINOBI_ENABLED=true
# Shinobi settings

# used for shinobi.domain.com/super
ADMIN_USER=admin@domain.com
ADMIN_PASSWORD=blahblahblah123456789

#I haven't tried these yet. Check MiGoller's docs
#CRON_KEY=b59b5c62-57d0-4cd1-b068-a55e5222786f
#PLUGINKEY_MOTION=49ad732d-1a4f-4931-8ab8-d74ff56dac57
#PLUGINKEY_OPENCV=6aa3487d-c613-457e-bba2-1deca10b7f5d
#PLUGINKEY_OPENALPR=SomeOpenALPRkeySoPeopleDontMessWithYourShinobi
#MOTION_HOST=localhost
#MOTION_PORT=80

# DB settings
# these value are used in initial setup and will persist in /lochnas/docker-data/shinobi/database
MYSQL_USER=shinobi
MYSQL_PASSWORD=blahblahblah1234567890
# Shinobi will use MYSQL_HOST to call the database. Set the database's container name to the same in docker-compose.yml
MYSQL_HOST=shinobi-db
MYSQL_DATABASE=ccio
MYSQL_ROOT_PASSWORD=blahblahblah1234567890
MYSQL_ROOT_USER=root

```

Finally run: `service lochnas restart`. Shinobi should be running now.

Check your logs with `journalctl -u lochnas.service` (and hit Shift+G to jump to the end). Run `docker ps -a` to ensure the Docker images `shinobi` and `shinobi-db` are running: 


### Setup Shinobi

Navigate in a browser to `shinobi.domain.com/super`. Log in using the credentials you set in .env (ADMIN_USER and ADMIN_PASSWORD). Add an account on the Accounts tab, and save it to your password manager.

Navigate in a browser to `shinobi.domain.com`. Log in using the account you just made.

Shinobi is running now! Read the Shinobi docs to continue.
