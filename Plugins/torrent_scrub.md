---
title: torrent_scrub
description: 
published: true
date: 2022-09-18T05:14:41.240Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:14:38.616Z
---

# Torrent metafile scrubber

Removes resume information and other non-standard data from torrent downloads. Note that this resume information prevents the torrent from properly starting in rTorrent, and is added by ruTorrent users if they incorrectly check the "Fast Resume" option while creating a torrent for uploading.


## Configuration

There is only one settings which determines what kind of metadata is removed from torrents:

| **Value** | **Description** |
| --- | --- |
| off | almost equivalent to commenting it out|
| on | normal scrubbing, all custom keys on top-level|
| all |  any custom key, also within the info dict; never use this on fresh downloads, it can modify the info hash |
| resume | just libtorrent fast-resume information), or `rtorrent` (any special Rtorrent metadata |
| rtorrent |  rTorrent users should this, so that incoming torrents never contain keys that modify the client's behaviour. |

Or you provide an explicit list of names you want to have removed; if they refer to inner dictionaries, use a dots to separate key names (e.g. `info.source`).



## Examples

To scrub one task:

```yaml
tasks:
  rutorrent-fast-resume-infected-task:
    torrent_scrub: rtorrent
```

If you want to be sure that all tasks are scrubbed, because you can never know, use this:

```yaml
templates:
  global:
    torrent_scrub: rtorrent
```

To scrub a list of keys you provide:

```yaml
torrent_scrub:
  - comment
  - info.source
```

Again, anything that changes the "info" dict, like the 2nd entry above, changes the info hash, which isn't wise for downloading purposes.
