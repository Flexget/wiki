---
title: delete
description: 
published: true
date: 2025-06-21T00:55:05.180Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:03:34.490Z
---

# Delete
Deletes files and/or directories from the local files ystem.

Syntax:

|Option|Description|
|---|---|
allow_dir | Allows the deletion of directories when set to true
along | Delete additional files such as subtitles while removing the main file.<br><br>Options:<br>*extensions* - file extensions to remove<br>*subdirs* - subdirectories to search in
clean_source | Delete this entry's parent directory if its size in MB is less than the supplied threshold after the deletion. Entry field `clean_source` can be used to override this value on a per entry basis.

Here is an example of usage in a more comprehensive context (untested)

```yaml
tasks:
  cleanup:
    filesystem:
      path: /filestorage1/
      recursive: yes
    age:
      field: created
      action: accept
      age: 600 days
    delete:
      clean_source: 1
      along:
        extensions:
          - sub
          - srt
```
