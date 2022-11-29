---
title: "LochNAS Setup Windows"
date: 2022-11-20
description: "How to setup LochNAS on windows"
tags: ["install", "setup", "windows"]
---

### Requirements
 - Windows is unknown and untested
 - root access
 - [Port forwarding](https://portforward.com/router.htm) 80 + 443
 - Static IP on Server, alternative is [DHCP reservation](https://portforward.com/dhcp-reservation/#how-to-make-a-dhcp-reservation-in-your-router) on router.
 - git
 - Docker Desktop

### Install

This is untested as of right now, See issue [#44](https://github.com/SiloCityLabs/lochnas/issues/44) for more information. You can manually install docker desktop and run `C:\lochnas\server.exe -daemon install`. You will need to manually compile this for Windows.

### Updates

LochNAS uses git to update. You can configure your update schedule via the `config.yml` file.

