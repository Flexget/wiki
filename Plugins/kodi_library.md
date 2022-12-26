---
title: kodi_library
description: 
published: true
date: 2022-12-03T03:42:34.131Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:07:12.176Z
---

# Kodi library
> **Requirements:** JSON-RPC must be enabled. See http://kodi.wiki/view/JSON-RPC_API#Enabling_JSON-RPC on how to enable it.
{.is-info}

Simple plugin to send clean or scan requests to a remote or local Kodi server. 
## Plugin Settings
Currently the following settings are supported:

|  Option  |  Description  |
| --- | --- |
| **action** | Can be either `scan` or `clean`. |
| **category** | The library type for which the action should be performed. Can be either `audio` or `video`. |
| **url** | URL to the Kodi webserver. |
| **port** (default 8080) | Port the Kodi webserver listens on. |
| **username** (optional) | Username for accessing the webserver. |
| **password** (optional) | Password for accessing the webserver. |
| **only_on_accepted** | Only send the request if entries were accepted (default `yes`). |

## Example
This plugin can be used in a move/sorting task in such way that Kodi scans for new video files after the moving/sorting is completed.

```yaml
tasks:
  organize_my_stuff:
    filesystem:
      ...
    move:
      ...
    kodi_library:
      action: scan
      category: video
      url: http://192.168.1.255
      port: 8080
```