---
title: "New Docker app"
date: 2022-11-29
description: "How to add new Docker application to LochNAS"
tags: ["apps"]
---

LochNAS is based on Docker and docker-compose YAML files. You can add your own Docker images and have them run on startup.

This guide assumes that you know how to use Docker Compose (docker-compose.yml files) and that you have a Docker image in mind. My _imaginary_ example is MyCoolApp which is (not actually) hosted on Dockerhub https://hub.docker.com/r/silocitylabs/mycoolapp

## Docker

To add a new application to LochNAS, create a new directory under /lochnas/docker-templates/ like `/lochnas/docker-templates/mycoolapp`. LochNAS will use this directory name later

In that directory create the files `docker-compose.yml`, `.env`, and `.example.env`

Configure `docker-compose.yml` with the image that you want to run. Ensure the Docker names are unique and don't interfere with LochNAS image names. If it uses volumes we recommend mapping to `/lochnas/docker-data/mycoolapp`

Here is a barebones `docker-compose.yml`
```
services:
    mycoolapp:
        container_name: mycoolapp
        image: silocitylabs/mycoolapp:latest
        restart: unless-stopped
        volumes:
            - '/etc/localtime:/etc/localtime:ro'
            - '/etc/timezone:/etc/timezone:ro'
        env_file:
            - /lochnas/docker-templates/mycoolapp/.env
        networks:
            - backend
```

The `.env` file should contain `MYCOOLAPP_ENABLED=true`. That name needs to match the directory name. When the variable equals **true**, LochNAS will start this docker-compose setup. The rest of `.env` can be filled with your application's environment viarables.

Copy `.env` to `.example.env`. Remove any passwords, API keys, etc so that you can share the example with others.

## Nginx

Use Nginx to access the image with a subdomain, like `mycoolapp.domain.com`. This part of the guide assumes that you already set up a [domain and DDNS](../ddns/)

First ensure that Nginx is enabled by editing `/lochnas/docker-templates/nginx/.env` and setting `NGINX_ENABLED=true`. Check the [Nginx docs](../../apps/nginx/)

Create a file `nginx.conf` in `/lochnas/docker-templates/mycoolapp`. You must write you configuration file from here. You may use ${GLOBAL_DOMAIN} to reference the domain set in `/lochnas/config.yml`

```
server {
    listen 443 ssl http2;
    server_name mycoolapp.${GLOBAL_DOMAIN};

......
```
