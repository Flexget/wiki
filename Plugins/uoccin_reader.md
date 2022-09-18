---
title: uoccin_reader
description: 
published: true
date: 2022-09-18T05:16:06.795Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:16:04.190Z
---

# Uoccin reader
This plugin synchronizes a local uoccin.json file with the updates coming from the [Uoccin](https://play.google.com/store/apps/details?id=net.ggelardi.uoccin) Android app via Google Drive.

## Plugin Settings
The following settings are supported:



|  Option  |  Description  |
| --- | --- |
| **uuid** | The machine identifier. Must be a simple but unique name, different for any device synchronizing on the same Google Drive account (i.e. "flexget_server", "home_pc1" etc). |
| **path** | This is the path to the uoccin.json file. |


### The task
Currently the task is required to be exactly like this:

```
uoccin_sync:
    seen: local
    filesystem:
      path:
        - path_to_uoccin_folder/device.this_machine_uuid'
      regexp: '.*\.diff$'
    accept_all: yes
    uoccin_reader:
      uuid: this_machine_uuid
      path: path_to_uoccin_folder
```

You just need to replace all the occurrences of **this_machine_uuid** with your chosen uuid, and all the occurrences of **path_to_uoccin_folder** with the real path in which resides the uoccin.json file.

**`IMPORTANT:`** The Android app can only be synchronized via Google Drive, so your uoccin.json file will reside in a folder named "uoccin" inside the root of your Google Drive folder.

Example real-word task:

```
uoccin_sync:
    seen: local
    filesystem:
      path:
        - C:\Users\Frank\Google Drive\uoccin\device.my_flexget_pc
      regexp: '.*\.diff$'
    accept_all: yes
    uoccin_reader:
      uuid: my_flexget_pc
      path: C:\Users\Frank\Google Drive\uoccin
```

  

