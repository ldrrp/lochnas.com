---
title: "LochNAS Setup"
date: 2022-11-20
description: "How to setup LochNAS for Ubuntu or Debian"
tags: ["install", "setup", "linux", "ubuntu", "debian"]
---

### Requirements
 - Ubuntu 20 server or greater is the preffered setup used for this system.
 - root user access
 - [Port forwarding](https://portforward.com/router.htm) 80 + 443
 - Static IP on Server, alternative is [DHCP reservation](https://portforward.com/dhcp-reservation/#how-to-make-a-dhcp-reservation-in-your-router) on router.
 - [Windows Guide](/docs/install-windows/) - Untested
 - [OSX Guide](/docs/install-osx) - Untested

### Install

Run the following command below

```bash
sudo curl -fsSL https://raw.githubusercontent.com/SiloCityLabs/lochnas/v3/install.sh -o install.sh && sudo sh install.sh
```

Edit your `config.yml` then restart `service lochnas restart`. If you are running your setup on a residential isp we recommend following our [ddns guide](/docs/ddns/).


### Updates

LochNAS uses git to update. You can configure your update schedule via the `config.yml` file.

### Commands

```
    server.bin -daemon
        start - Start in background
        stop - Stop background
        restart - restart in background
        install - Install as service
        uninstall - Uninstall service
    server.bin -ddns
        ip - Grab current wanip from router
        refresh - update ddns if ip changed
        force - Force update ddns ip
    server.bin -domain
        renew - Renew all domains
        add - Renew all domains, expects domain as argument
        delete - Renew all domains
    server.bin -apps
        update - Update
    server.bin -server
        notify - Send test notifications
    server.bin -config /path/to/alt/config
```

### Create users and groups  (optional)

This portion is handled by the containers but in some instances file permissions may have changed. We will be using the www-data user to share permissions between services. You can make seperate users and groups if you would like to but I found that this is the easiest way to manage access accross the board.

You can give your user access to any files of www-data with this command.

```
usermod -aG www-data yourusername
```

If you need to access the local folder mounted in the compose file at `/lochnas/home` from nextcloud local storage plugin, you can run the following set of commands on a folder to grant permission:

```
chown -R www-data:www-data /lochnas/home
chmod -R 770 /lochnas/home
```


### Apps

You can view our list of [apps](/apps/) to get started. We recommend activating [nginx](/apps/nginx/) first.
