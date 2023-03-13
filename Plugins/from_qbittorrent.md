---
title: from_qbittorrent
description: 
published: true
date: 2023-03-13T10:36:35.309Z
tags: dependencies
editor: markdown
dateCreated: 2023-02-22T02:23:13.583Z
---

# From QBittorrent
This plugin creates an entry for each item you have loaded in qbittorrent.

> This plugin requires the `qbittorrent-api` library. 
{.is-warning}

To install it, run:
```cmd
pip install qbittorrent-api
```

## Options

| **Name** | **Info** | **Description** |
| --- | --- | --- |
| host | Text | Where qbittorrent is listening |
| port | Number | Connected port  |
| username | Text |  |
| password | Text |  |
| category | Text | Create entries only from given category name |
| completed | [yes\|no] | Create only completed torrents |

## Provides entry fields

- content_files
- content_size
- torrent_info_hash
- torrent_info_hash_v2
- torrent_seeds
- torrent_peers
- qbittorrent_ratio
- qbittorrent_category
- qbittorrent_state
- qbittorrent_eta
- qbittorrent_added_on
- qbittorrent_completion_on
- qbittorrent_completed_path
- qbittorrent_download_path
- qbittorrent_save_path
- qbittorrent_size
- qbittorrent_dl_speed
- qbittorrent_up_speed
- qbittorrent_is_checking
- qbittorrent_is_complete
- qbittorrent_is_downloading
- qbittorrent_is_errored
- qbittorrent_is_paused
- qbittorrent_is_uploading



**Example:**

```
from_qbittorrent:
  host: localhost
  port: 8081
  username: myusername
  password: mypassword
```