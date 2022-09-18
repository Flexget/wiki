---
title: RemoveByExtension
description: 
published: true
date: 2022-09-18T05:20:58.383Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:20:55.765Z
---

Sometimes the content-filter does not work and you end up with *.wmv -files that often are fake episodes

This task-recipe removes the files and creates a script to forget the episodes

this config does not work on Windows, You'd have to make the exec-plugin create a bat-file.. but the concept is the same

execute like this (on linux)
```
flexget execute --tasks unwanted-series && /your_dir/cleanup.sh
```

But first, put this in your config

```
tasks:
  unwanted-series:
    manual: yes
    disable_builtins: [seen](/seen)
    metainfo_series: yes
    accept_all: yes
    filesystem:
      regexp: .*(wmv)$
      path: /media/Video/TV-Series
      recursive: yes

    move:
      to: /dev/null  #Or if you are not that brave /some_dir/fakes
      filename: '{{ series_name }} - {{ series_id }}{{location | pathext}}'
      along:
        - srt
        - txt
      clean_source: 5

    exec:
      on_start:
        phase: echo "#!/bin/bash" > /root/cleanup.sh && chmod +x /your_dir/cleanup.sh
      on_output:
        for_accepted: echo "flexget series forget \"{{series_name}}\" S{{series_season|pad(2)}}E{{series_episode|pad(2)}}" >> /your_dir/cleanup.sh
```