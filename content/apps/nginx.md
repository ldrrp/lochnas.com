---
title: "Nginx"
date: 2022-11-30
description: "Web server that can also be used as a reverse proxy, load balancer, mail proxy and HTTP cache"
tags: ["apps", "docs", "nginx", "http", "proxy"]
---

## Details

This container allows you to server all your containers trhough port 443 via ssl with only a single port forward set in your router.

## How to enable

Edit your `/lochnas/docker-templates/nginx/.env` file and enable this container with `NGINX_ENABLED=true` and other variables. 

It is recommended you set a password for auth enabled applications to use by uncommenting the following two options in the nginx `.env` file.

```
NGINX_PASSWORD={password}
NGINX_USERNAME=admin
```

## SSL Certificates

## Add a domain ssl

You need to use the domain argument to create SSL certificates for your nginx setup. This is highly recommended and uses Let's Encrypt for a valid certificate for free. Create your first root domain here for nginx to use as the default. Each app may need its own domain specified in its docs.

```
/lochnas/server.bin -domain add domain.com
```

## Delete a domain ssl

```
/lochnas/server.bin -domain remove
```

## Renew domain ssl's

This happens automatically but you can manually trigger it with the following command.

```
/lochnas/server.bin -domain renew
```