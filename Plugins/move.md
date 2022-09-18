---
title: move
description: 
published: true
date: 2022-09-18T05:08:19.487Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:08:16.895Z
---

# Move

### Syntax:

|Option|Description|
|---|---|
|to| Directory to move accepted entries to, allows value replacement, defaults to download path. Entry field `move_to` can be used to override given path per entry basis.|
|rename| The actual filename inside the 'to' directory to rename the entries, allows value replacement|
|allow_dir| Allows or denies to operate on entries pointing to directories|
|keep_extension | Enable or disable automatic adding of extension (e.g. .torrent) to renamed file. Default: Yes
|unpack_safety | Enable or disable unpacking safety checks, enabled by default. causes 1 sec delay per processed entry|
|clean_source| Delete source directory if it has less MB left than given after move
|along|Move additional files such as subtitles<br><br>[extensions]: file extensions<br>[subdirs]: sub directories to search in|

**NOTE** : It is important to note that the files are moved as single files and no checks are made if multiple files match the same name. The files already present in the directory (even if moved during the same pass) are overwritten.

### Examples

#### Organize series

```yaml
tasks:
  move-episodes:
    metainfo_series: yes 
    accept_all: yes 
    filesystem:
      path: /downloads/
      recursive: yes 
    move:
      to: '/storage/{{series_name}}/'
      rename: '{{ series_name }} - {{ series_id }}{{ location|pathext }}'
      along:
        extensions:
          - sub
          - srt
        subdirs:
          - Subs
```

