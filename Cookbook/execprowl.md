---
title: execprowl
description: 
published: true
date: 2022-09-18T04:56:49.586Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:56:46.899Z
---

# Use exec and curl to send a Prowl notification
**DEPRECATED**

Use [prowl](/Plugins/prowl) plugin instead!

If you have the iPhone app Prowl, you can use the exec plugin and curl to send notifications.

## Example
```
exec: 'curl -k https://prowl.weks.net/publicapi/add -F apikey=XXXXXXXXX -F application="FlexGet" -F description="%(series_name)s %(series_season)sx%(series_episode)s %(feed)s" '
```

In the exec command `%(series_name)s %(series_season)sx%(series_episode)s %(feed)s` will be replaces with the parsed series name and season information assuming you also use the series plugin.

You will need to replace XXXXXXXXX with your prowl api key.

More information about prowl can be found at https://prowl.weks.net/

[Back to The Cookbook](/Cookbook)