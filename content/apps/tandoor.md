---
title: "Tandoor"
date: 2025-01-10
description: "The recipe manager that allows you to manage your ever growing collection of digital recipes."
tags: ["apps", "docs", "tandoor", "food", "recipes"]
---

## Details

This is a template to add this container to your nas setup full functional with matching permissions and settings that of lochnas repo.

## How to enable

Add the domain ssl replacing domain.com with the root domain you entered in your config.yml

```
/lochnas/server.bin -domain add tandoor.{domain.com}
```

Edit your `/lochnas/docker-templates/tandoor/.env` file and enable this container with `TANDOOR_ENABLED=true` and other variables. You can access it via https://tandoor.yourdomain.com

To use web access you must have nginx auth password set

## Additional Configuration
