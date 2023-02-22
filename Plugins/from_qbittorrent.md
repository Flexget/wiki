---
title: from_qbittorrent
description: 
published: true
date: 2023-02-22T02:23:13.583Z
tags: 
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
| host | Text | Where transmission is listening (default: localhost) |
| port | Number | Connected port (default: 9091) |
| username | Text |  |
| password | Text |  |
| password | Text | Create entries only from given category name |
| completed | [yes\|no] | If this is enabled, only completed torrents have entries created. |


**Example:**

```
from_qbittorrent:
  host: localhost
  port: 8081
  username: myusername
  password: mypassword
```