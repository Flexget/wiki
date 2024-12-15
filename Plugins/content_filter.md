---
title: content_filter
description: 
published: true
date: 2024-12-15T03:08:03.977Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:02:56.562Z
---

# Content Filter
This allows filtering based on the filenames inside of torrents.
> This plugin does not accept entries on its own, only rejects already accepted entries that do not pass your requirements. You'll need another [filter plugin](/Plugins#Filters) in the task to accept the entries you want.
{.is-info}

> `content_filter` doesn't work with magnet links, as it works by analyzing the file list present in the .torrent file. You can include the [magnets](/Plugins/magnets) plugin to reject any magnet entries.
{.is-warning} 
 
 |---|---|---|
 | Field | Default | Description |
 | `require` | `None` | Reject the entry if **none** of the files in the torrent matches **any** of the masks |
 | `reject` | `None` | Reject the entry if **any** of the files in the torrent matches **any** of the masks |
 | `require_all` | `None` | Reject the entry if **all** of the masks **do not** match across the files in the torrent |
 | `reject_all` | `None` | Reject the entry if **all** of the masks **do** match across the files in the torrent |
 | `require_mainfile` | `false` | Reject the entry unless the torrent contains a single file or one of the files accounts for at least 90% of the size |
 | `strict` | `false` | Reject the entry if `content_filter` is unable to parse the torrent files |
 | `regexp_mode` | `false` | Switches filename matching from filesystem patterns to case-insensitive Regular Expressions |

For the requirement and rejection fields, you can specify a single mask, a list of masks or an input plugin.



## Examples
- Reject torrents that do not have mkv file in them:
```
content_filter:
  require: '*.mkv'
```
- Reject torrents that have rars in them:

```
content_filter:
  reject: '*.rar'
```
- Reject torrent if it doesn't have mp4 OR mkv in it. Reject also if there are wmv files
```
content_filter:
  require:
    - '*.mp4'
    - '*.mkv'
  reject: '*.wmv'
```
- Reject torrents that don't have a matroska container AND a nfo file:
```
content_filter:
  require_all: 
    - '*.mkv'
    - '*.nfo'
```
- Reject multifile torrents that don't have one file at least 90% of total size (single-file torrents are not affected)
```
content_filter:
  require_mainfile: yes
```
- Reject torrent if none of its files match any of the entries in a previously populated [`regexp_list`](/Plugins/List/regexp_list)
```
content_filter:
  regexp_mode: yes
  require:
    from:
      - regexp_list: my-wanted-files
```