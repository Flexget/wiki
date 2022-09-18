---
title: abort_if_exists
description: 
published: true
date: 2022-09-18T05:01:38.837Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:01:36.304Z
---

# Abort If Exists
Abort the running task if the specified field in an entry matches the regexp. This is useful when moving local files around and a program is currently transferring data to the disk.

```TEXT
abort_if_exists:
  regexp: <regexp>
  field: <field name>
```
### Example

Abort the task if [lftp](https://lftp.yar.ru/) is currently transferring data. 

```yaml
tasks:
  example_task:
    filesystem:
      path:
        - /storage/movies/
        - /storage/tv/
      recursive: yes
      retrieve: files
      regexp: '.*\.(avi|mkv|mp4|lftp-get-status)$'
    abort_if_exists:
      regexp: '.*\.lftp-get-status$'
      field: location
```