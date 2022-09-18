---
title: qbittorrent
description: 
published: true
date: 2022-09-18T05:10:26.882Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:10:24.266Z
---

# qBittorrent
Downloads content from entry URL and loads it into the  qBittorrent bittorrent client.

Requirements: Supports qBittorrent 3.1.3 and above. qBittorrent WebUI must be enabled in the options menu.

## Options

All options are optional and will default to whatever you have set in qBittorrent. If you wish not to set any of the parameters the format is:

```yaml
qbittorrent: yes
```

**Options**

|  Name  |  Description  |
| --- | --- |
| host | qBittorrent host (default *localhost*)  |
| port | qBittorrent port (default *8080*)  |
| username | qBittorrent username that was set in the WebUI options. Can be omitted if *Bypass authentication for localhost* is checked  |
| password | qBittorrent password that was set in the WebUI options. Can be omitted if *Bypass authentication for localhost* is checked |
| use_ssl | Connect to the provided hostname using https (default *False*)
| verify_cert | Enable or disable SSL certficate verification (default *True*)
| path | The download location |
| label | Assigns corresponding qBittorrent label/category |
| tags | Assign one or more tags to torrent. Can be used both in config and in a task.
| maxdownspeed | Set torrent download speed limit. Unit in kilobytes/second |
| maxupspeed | Set torrent upload speed limit. Unit in kilobytes/second |
| add_paused | Add torrents in the paused state (default: *False*)|
| skip_check | Skip initial hash check (default: *False*)|

### Examples

```yaml
qbittorrent:
  path: /media/disk/downloads/
  label: tv
  host: localhost
  port: 8080
  tags:
    - flexget
```

Dynamically set tags

```yaml
tasks
  movies:
    set:
      tags:
        - '{quality.resolution}'

```