---
title: "Portainer"
date: 2022-11-29
description: "Hybrid & multi-cloud container management platform"
tags: ["apps", "docs", "portainer"]
---

## Details

This is a template to add this container to your nas setup full functional with matching permissions and settings that of lochnas repo.

Original maintainer [portainer/portainer-ce](https://hub.docker.com/r/portainer/portainer-ce)

## How to enable

Edit your `/lochnas/docker-templates/portainer/.env` file and enable this container with `PORTAINER_ENABLED=true`

After running `service lochnas restart` navigate in a browser to configure at `portainer.domain.com`. Create a username and password, then select local docker and hit next. You should be complete.