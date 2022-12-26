---
title: btn
description: 
published: true
date: 2022-12-07T05:41:04.580Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:17:14.052Z
---

# BTN
> This plugin is part of [search](/Plugins/Searches) plugin system
{.is-success}

This search plugin will get series episode results from torrent site BTN. There is a limit of 150 api calls per hour, so make sure you do not schedule tasks using this to run too often.

## Configuration
Configuration requires just api key, which can be found by going to the edit profile section on BTN.
```
btn: apikey
```
Some releases on BTN do not include quality tags (anime in particular) and the quality is therefore appended to the title. This means that for a lot of releases, the quality tags will be present twice in the title. This can be turned off with the alternate config:
```
btn:
  api_key: apikey
  append_quality: yes|no (default yes)
  origin: string or list (see below)
```

### Origins
Plugin can be configured to filter the search based on "origin":

    'None'
    'Scene'
    'P2P'
    'User'
    'Mixed'
    'Internal'