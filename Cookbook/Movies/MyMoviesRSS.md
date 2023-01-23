---
title: MyMoviesRSS
description: 
published: true
date: 2023-01-23T16:49:05.522Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:19:58.005Z
---

## My movie list
Generates RSS with Imdb details, ordered by imdb score. Throw in [imdb_rated](/Plugins/imdb_rated) and you get list of unwatched movies!

```yaml
templates:
  generate:
    interval: 4 hours
    accept_all: yes
    imdb_lookup: yes
    disable_builtins: yes
    sort_by:
      field: imdb_score
      reverse: yes

tasks:

  rss-unwatched:
    template: generate
    filesystem: /storage/movies/
    make_rss:
      file: ~/public_html/movies.rss
      history: no
```

Uses plugins: [template](/Plugins/template), [imdb_lookup](/Plugins/imdb_lookup), [make_rss](/Plugins/make_rss), [filesystem](/Plugins/filesystem)