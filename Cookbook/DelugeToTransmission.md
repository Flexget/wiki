---
title: DelugeToTransmission
description: 
published: true
date: 2022-09-18T04:55:17.414Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:55:14.914Z
---

# Transfer torrents from deluge to transmission
```yml
tasks:
  migrate_deluge:
    manual: yes # do not run this task automatically - only with flexget execute --tasks migrate_deluge
    from_deluge:
        config_path: "/home/username/.config/deluge" # you need to change path to another one - check your deluge config
    set:
      path: "{{deluge_path}}" # to be sure that transmission downloads to the same path as deluge
    seen: local
    accept_all: yes
    deluge: no
    transmission: yes # you may need to setup connection info here
    disable:
      - seen
      - seen_info_hash
```