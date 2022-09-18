---
title: web
description: 
published: true
date: 2022-09-18T04:54:51.188Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:54:48.600Z
---

## [CLI](/CLI) > `web`
Manage web server settings

### Positional arguments
| Argument | Option | Description |
| --- | --- | --- |
| `passwd` || change password for web server |
|| `<new_password>` | New password |
| `gentoken` || Generate a new api token |
| `showtoken` || Show api token |

### Examples
```bash
#shows the FlexGet web server API token
$ flexget web showtoken

#changes the password to foopass
$ flexget web passwd foopass
```