---
title: "Nextcloud"
date: 2022-11-29
description: "On-premises personal cloud interface"
tags: ["apps", "docs", "nextcloud"]
---

## Details

This is a template to add this container to your nas setup full functional with matching permissions and settings that of lochnas repo. If you havent already done so you must enable [nginx](/apps/nginx/) container first.

Original maintainer [Nextcloud](https://hub.docker.com/_/nextcloud), [mariadb](https://hub.docker.com/_/mariadb)

## How to enable

Add the domain ssl replacing domain.com with the root domain you entered in your config.yml

```
/lochnas/server.bin -domain add cloud.{domain.com}
```

Edit your `/lochnas/docker-templates/nextcloud/.env` file and enable this container then run `service lochnas restart`

```
NEXTCLOUD_ENABLED=false
NEXTCLOUD_DATA=/lochnas/home
MYSQL_ROOT_PASSWORD=password
MYSQL_PASSWORD=password
```

### Setup nextcloud

Navigate in a browser to configure nextcloud at `cloud.domain.com`

First enter a personal username and password to login to nextcloud. Then before hitting next hit the advanced option.

 - Click `MySQL / MariaDB`
 - Leave data path default
 - Database User: `nextcloud`
 - Database Password: password from .env `MYSQL_PASSWORD=`
 - Database Name: `nextcloud`
 - Change `localhost` to `mariadb:3306`
 - Click `Next`
 
Note: If you get the error `504 Gateway timeout`, edit the file `docker-data/nextcloud/html/config/config.php` and remove `:3306` from `dbhost` and add it to `dbport` as `3306`. This is an unfortunate bug in the nextcloud installer but shouldnt be an issue past this.

After you get to the welcome screen go to settings -> basic settings. Change the cron settings to webcron. 

Go to apps and disable the app called `Deleted Files`. This application causes issues with `External Storage` plugin.

Go to External storage in settings and create a storage under /raid for your users.

You will need to make some tweaks to improve this nextcloud docker setup. Type the following commands:

```bash
docker exec -u www-data -it nextcloud ./occ db:add-missing-indices
docker exec -u www-data -it nextcloud ./occ db:convert-filecache-bigint
docker exec -u www-data -it nextcloud ./occ config:app:set text workspace_available --value=0
```

Make one last addition to the config file to fix a login redirect issue.

`nano docker-data/nextcloud/html/config/config.php`
```
  'overwrite.cli.url' => 'https://cloud.yourdomain.com',
  'overwritehost' => 'cloud.yourdomain.com',
  'overwriteprotocol' => 'https',
```

### Stuck in Maintenance mode

Sometimes Nextcloud finds itself stuck unable to update due to an issue. You can run the command to determine why its stuck.

```bash
docker exec -it -u 33 nextcloud php occ upgrade
```

If you see an error like "Cannot skip major versions". You will need to download the previous version and upgrade incrimentally. The following example goes from 23 -> 24. You will need to repeat this for multiple major versions.

```bash
cd /lochnas/docker-data/nextcloud
cat html/config/config.php | grep version
mv html nextcloud
wget https://download.nextcloud.com/server/releases/nextcloud-24.0.0.zip
unzip -o nextcloud-24.0.0.zip
mv nextcloud html
docker exec -it -u 33 nextcloud php occ upgrade
```