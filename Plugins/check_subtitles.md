---
title: check_subtitles
description: 
published: true
date: 2022-09-18T05:02:47.620Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:02:45.055Z
---

# Check subtitles
Set the **subtitles** field on all [entries](/Entry) about local files having subtitles. The field is a list of available languages.

### Example
```
check_subs:
    filesystem:
      path:
        - D:\Media\Incoming\series
      regexp: '.*\.(avi|mkv|mp4)$'
      recursive: yes
    check_subtitles: yes
    if:
      - "subtitles and 'ita' in subtitles": accept
```