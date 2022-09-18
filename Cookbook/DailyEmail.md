---
title: DailyEmail
description: 
published: true
date: 2022-09-18T05:04:35.616Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:55:07.345Z
---

# Send daily email of accepted downloads
This will produce a daily email containing all downloads accepted from multiple different tasks. The email will be sent once per day no matter how often flexget is executed. You insert the [digest](/Plugins/digest) plugin on whatever tasks you want to collect into the email. The [emit_digest](/Plugins/emit_digest) plugin is used in another task to output all the entries captured by the digest plugin, and should be configured with the same list name as you used for the digest plugin. 

```
tasks:
  task-a:
    rss: http://something.com/feed.rss
    digest: daily email
    series:
      - good show

  task-b:
    rss: http://somethingelse.com/feed.rss
    digest: daily email
    series:
      - other show

  daily-email:
    interval: 1 days
    emit_digest:
      list: daily email
    seen: local
    accept_all: yes
    email:
      from: xxx@xxx.xxx
      to: xxx@xxx.xxx
      smtp_host: smtp.host.com
      smtp_port: 25
      smtp_login: true
      smtp_username: my_smtp_login
      smtp_password: my_smtp_password
```
