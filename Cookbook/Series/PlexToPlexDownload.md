---
title: PlexToPlexDownload
description: 
published: true
date: 2022-09-18T05:20:46.828Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:20:44.314Z
---

This recipe allows you to download the latest episodes from a remote PMS by using a section from your local PMS to configure the series plugin.


```
import_series:
  from:
    plex:
      server: 192.168.0.20
      section: 3  
plex:
  section: 3
  server: 111.222.333.444
  selection: recentlyAdded
  username: myplexusername
  password: myplexpassword
download:
  path: /mnt/tv/{{series_name|replace(' ', '.')|lower}}/{% if series_season %}s{{series_season|pad(2)}}{%endif%}
```
