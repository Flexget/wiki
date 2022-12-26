---
title: filelist
description: 
published: true
date: 2022-12-07T05:48:24.092Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:17:34.076Z
---

# FileList
> This plugin is part of [search](/Plugins/Searches) plugin system
{.is-success}

> This plugin will be deprecated with the next flexget release please consider using the new <a href="https://flexget.com/Searches/filelist_api">filelist_api</a>. Also since the .ro domain stopped working this plugin is broken.
{.is-danger}

This search plugin will get results from [filelist.ro](https://filelist.ro).

## Configuration
Requires username, password and passkey. Passkey can be retrieved from [here](https://filelist.ro/getrss.php).
```
filelist:
  username: xxxxxxx
  password: xxxxxxx
  passkey: xxxxxx
  category: <one category from the list below>
  include_dead: yes|no # include dead torrents
  order_by: hybrid|relevance|date|size|snatches|peers # default is hybrid
  order_ascending: yes|no
  search_in: title|description # if not specified, it searches in both
```

*Important note: FileList only lets you search in a single category*

**Categories**
* all
* anime
* audio
* cartoons
* docs
* games console
* games pc
* linux
* misc
* mobile
* movies 3d
* movies bluray
* movies dvd
* movies dvd-ro
* movies hd
* movies hd-ro
* movies sd
* series hd
* series sd
* software
* sport
* tv
* videoclip
* xxx

## Example Usage

```
tasks:
  get-series:
    series:
      - House
    discover:
      what:
        - emit_series: yes
    from:
      - filelist:
          username: '{% variables.fl.username %}'
          password: '{% variables.fl.password %}'
          passkey: '{% variables.fl.passkey %}'
          category: series hd
```

## Misc.
FileList plugin includes extra information about torrents in the search result, which are available in entry fields.

* torrent_internal (boolean)
* torrent_freeleech (boolean)

Following example rejects torrents that are not freeleech.
```
tasks:
  get-series:
    series:
      - House
    discover:
      what:
        - emit_series: yes
    from:
      - filelist:
          username: '{% variables.fl.username %}'
          password: '{% variables.fl.password %}'
          passkey: '{% variables.fl.passkey %}'
          category: series hd
    if:
      - not torrent_freeleech: reject
```