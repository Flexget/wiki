---
title: argenteam
description: 
published: true
date: 2022-12-07T05:16:18.924Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:17:06.213Z
---

# aRGENTeaM

> This plugin is part of [search](/Plugins/Searches) plugin system
{.is-success}

Retrieves results from [www.argenteam.net](http://www.argenteam.net/), latin american (Argentina) web.

Add an entry field `argenteam_subtitle`, which contains subtitle’s url.
### Configuration
| Option | Description |
| --- | --- |
| force_subtitles | `yes` or `no`. Force download release with subtitles made by aRGENTeaM. Default is `yes`|

### Examples
#### Simple download
```
argenteam:
    force_subtitles: yes
```

#### Download video and subtitles
```
argenteam:
    force_subtitles: yes
exec: ./argenteam_download_subtitle.sh '{{argenteam_subtitle}}' /downloads/transmission >> argenteam_subtitles.log
```
##### Script to download
argenteam_download_subtitle.sh
```
wget "$1" -qO subs.zip
unzip -o subs.zip -d "$2"
rm subs.zip
```