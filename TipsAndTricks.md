---
title: TipsAndTricks
description: 
published: true
date: 2022-09-18T04:52:04.507Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:52:01.842Z
---

# Advanced Tips And Tricks
Here you can find some advanced YML configuration tricks. Check [global section](/GlobalSection) for some tips as well. These are mainly for those who really like to tinker with application.

## Defining download paths as variables (yaml-references)
In case you have multiple download locations, or path is long, you may wish to use variables instead of typing full path on each download location.

Example:

```
series: &series ~/torrents/series
movies: &movies ~/torrents/movies

feeds:
  feed A:
    download: *movies
  feed B:
    download: *movies
  feed C:
    download: *series
  feed D:
    download: *movies
    patterns:
      - pattern A
      - pattern B: *series
      - pattern C
```

Variables can also be defined on their first occurrence and then reused as needed.

```
---
feeds:
  feed A:
    download: &movies ~/torrents/movies
  feed B:
    download: *movies
  feed C:
    download: &series ~/torrents/series
  feed D:
    download: *movies
    patterns:
      - pattern A
      - pattern B: *series
      - pattern C
...
```

## Extending feed configuration
In case you have similar feed configurations you can use use one of them as template, or create separate non-used template outside feeds list.

Example:

```
feeds:
  feed A: &movies
    rss: http://some.site.com/rss.php
    patterns:
      - pattern A
      - pattern B
    download: ~/movies/

  feed B:
    rss: http://somewhere.else.com/rss.php
    <<: *movies
```

In above example `feed B` also has everything configured in `feed A`, but the rss value has been overwritten with another site.

## Disable feeds without commenting them out
You can disable feeds temporarily by prefixing names with _ character. This is much easier than commenting out all lines.