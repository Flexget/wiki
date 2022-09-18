---
title: uoccin_collection
description: 
published: true
date: 2022-09-18T05:15:55.129Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:15:52.503Z
---

# Uoccin collection add/remove
The `uoccin_collection_add` plugin marks the accepted movies and/or episodes as collected (downloaded) in your local uoccin.json file and update the [Uoccin](https://play.google.com/store/apps/details?id=net.ggelardi.uoccin) Android app database (if you are using it).

The `uoccin_collection_remove` plugin do the opposite: clear the collected flag.

## Plugin Settings
The following settings are supported:



|  Option  |  Description  |
| --- | --- |
| **uuid** | The machine identifier. Must be a simple but unique name, different for any device synchronizing on the same Google Drive account (i.e. "flexget_server", "home_pc1" etc). |
| **path** | This is the path to the uoccin.json file. |


### Example:
This example shows how the uoccin_collection_add plugin could be used with the [from_transmission](/Plugins/from_transmission) plugin to mark the download episodes as collected.

```
move_episodes:
    metainfo_series: yes
    thetvdb_lookup: yes
    from_transmission:
      enabled: yes
      port: 9092
      onlycomplete: yes
    if:
      - not (location and 'series' in location): reject
    uoccin_collection_add:
      uuid: this_machine_uuid
      path: path_to_uoccin_folder
```
  
**`IMPORTANT:`** The Android app can only be synchronized via Google Drive, so your uoccin.json file will reside in a folder named "uoccin" inside the root of your Google Drive folder.