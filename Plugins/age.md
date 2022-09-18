---
title: age
description: 
published: true
date: 2022-09-18T05:05:09.921Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:01:51.243Z
---

# Age
Simple plugin to filter based on age. The age is determined via a date set in an entry field. It can for example be used in conjunction with entries created by [filesystem](/Plugins/filesystem), which sets the fields `accessed`, `modified`, `created`, which are last accessed, last modified and file creation respectively.

## Plugin settings
Currently the following settings are supported:


|  Option  |  Description  |
| --- | --- |
| **field** | Entry field. The date in this field must be ISO 8601 compliant or a Python datetime object. |
| **age** | The age to be filtered. Format: [n] [minutes&#124;hours&#124;days&#124;months] eg. `7 days`. |
| **action** | Action to perform on entries. Either `accept` or `reject`. |

## Examples
Example task to delete video files that have not been accessed in the last 7 days:

```yaml
tasks:
  delete_by_age:
    filesystem:
      path:
        - /some/path
      regexp: '.*\.(avi|mkv|mp4)$'
      recursive: yes
      retrieve: files
    age:
      field: accessed
      action: accept
      age: 7 days
    delete:
      clean_source: 1
      along:
        - sub
        - srt
```
