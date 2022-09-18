---
title: irc
description: 
published: true
date: 2022-09-18T05:24:19.841Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:53:58.170Z
---

## [CLI](/CLI) > `irc`
View and manage [IRC connections](/Plugins/Daemon/irc).

### Actions
| action | option | description |
| --- | --- | --- |
| `status` || Shows status for a specific IRC connection |
|| *positional:* ||
|| `<irc_connection>` | Title of the IRC connection |
| `restart` || Restart an IRC connection |
|| *positional:* ||
|| `<irc_connection>` | Title of the IRC connection |
| `stop` || Stops an irc connection |
|| *positional:* ||
|| `<irc_connection>` | Title of the IRC connection |


### Examples
```bash
#shows the status for a specific irc connection
$ flexget irc status
```