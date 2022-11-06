---
title: from_transmission
description: 
published: true
date: 2022-11-06T14:38:15.952Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:05:55.831Z
---

# From Transmission
This plugin creates an entry for each item you have loaded in transmission.

> This plugin requires the transmission-rpc library. To install it, run:
{.is-info}

```
pip install transmission-rpc
```

You may be required to upgrade transmission-rpc after upgrading transmission, for that just add `--upgrade` to the previous command.
</div>

**Example:**

```
from_transmission:
  host: localhost
  port: 9091
  username: myusername
  password: mypassword
```


| **Name** | **Info** | **Description** |
| --- | --- | --- |
| host | Text | Where transmission is listening (default: localhost) |
| port | Number | Connected port (default: 9091) |
| netrc | File |  |
| username | Text |  |
| password | Text |  |
| only_complete | [yes\|no] | If this is enabled, only completed torrents, which have also finished their seeding requirements will have entries created. |
