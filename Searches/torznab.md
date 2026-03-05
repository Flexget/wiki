---
title: torznab
description: 
published: true
date: 2026-03-05T14:45:11.980Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:19:07.131Z
---

# torznab
Designed to search using Torznab indexers with with [discover](/Plugins/discover) plugins. Tested using [Jackett](https://github.com/Jackett/Jackett), though should work with any Torznab indexer.

## Config format
```text
discover:
  what:
    - ...
  from:
    - torznab:
        url: <torznab service url>
        [apikey]: <apikey>
        [searcher]: <value>
        [categories]: <values>
```
| Option | Default | Description |
| --- | --- | --- |
|searcher| search | Can be `movie`, `tv`, `tvsearch` or `search`. <br/><br/>`tv` and `tvsearch` are aliases.<br/>`tv` and `movie` both take advantage of metadata provided by torznab feeds and matches the results with metadata available in the flexget entry already (trakt_id, imdb_id, etc.).<br/>`search` is a simple search without the additional checks described above. |
|categories| -| List of znab categories to restrict the search to, see [newznab documentation](https://newznab.readthedocs.io/en/latest/misc/api/#predefined-categories) for the category ids. |


## CLI

Query url capabilities for torznab. For example bitmagnet.

```bash
$ flexget torznab "http://192.168.x.x:3333/torznab"

Server: bitmagnet
Limits: max=100, default=100

Searching capabilities:
  ✓ search: yes
    Supported params: q,imdbid,tmdbid
  ✓ tv-search: yes
    Supported params: q,imdbid,tmdbid,season,ep
  ✓ movie-search: yes
    Supported params: q,imdbid,tmdbid
  ✓ music-search: yes
    Supported params: q
  ✗ audio-search: no
  ✓ book-search: yes
    Supported params: q

Categories:
  2000: Movies
    └─ 2030: Movies/SD
    └─ 2040: Movies/HD
    └─ 2045: Movies/UHD
    └─ 2060: Movies/3D
  3000: Audio
    └─ 3030: Audio/Audiobook
  4000: PC
    └─ 4050: PC/Games
  5000: TV
    └─ 5030: TV/SD
    └─ 5040: TV/HD
    └─ 5045: TV/UHD
  6000: XXX
    └─ 6070: XXX/Other
  7000: Books
    └─ 7020: Books/EBook
    └─ 7030: Books/Comics
  8000: Other
```  

## Examples
### Search for movies from trakt watchlist
```yaml
tasks:
  discovermovies:
    discover:
      what:
        - trakt_list:
            username: <trakt username>
            account: <account set up in CLI>
            list: watchlist
            type: movies
      from:
        - torznab:
            url: http://jackett:9117/api/v2.0/indexers/all/results/torznab/
            apikey: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
            searcher: movie
    accept_all: yes
    trakt_lookup: yes
    quality: 1080p+
    duplicates:
      field: imdb_id
      action: reject
    sort_by:
      - quality
      - torrent_availability
      - torrent_seeds
    transmission:
      username: transmission
      add_paused: Yes
```
### Search for HD tv shows
```yaml
torznab:
  url: http://jackett:9117/api/v2.0/indexers/all/results/torznab/api
  apikey: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
  searcher: tv
  categories:
    - 5040
```