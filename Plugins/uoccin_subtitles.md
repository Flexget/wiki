---
title: uoccin_subtitles
description: 
published: true
date: 2022-09-18T05:16:10.667Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:16:08.075Z
---

# Uoccin subtitles
This plugin only purpose is to update the [Uoccin](https://play.google.com/store/apps/details?id=net.ggelardi.uoccin) Android app about the subtitles downloaded.

## Plugin Settings
The following settings are required:



|  Option  |  Description  |
| --- | --- |
| **uuid** | The machine identifier. Must be a simple but unique name, different for any device synchronizing on the same Google Drive account (i.e. "flexget_server", "home_pc1" etc). |
| **path** | This is the path to the uoccin.json file. |


### Example:
```
get_series_subs:
    metainfo_series: yes
    thetvdb_lookup: yes
    filesystem:
      path:
        - path_to_tv_shows
      regexp: '.*\.(avi|mkv|mp4)$'
      recursive: yes
    subliminal:
      languages:
        - ita
      alternatives:
        - eng
    uoccin_subtitles:
      uuid: this_machine_uuid
      path: path_to_uoccin_folder
```
  
**`IMPORTANT:`** The Android app can only be synchronized via Google Drive, so your uoccin.json file will reside in a folder named "uoccin" inside the root of your Google Drive folder.