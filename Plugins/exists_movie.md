---
title: exists_movie
description: 
published: true
date: 2025-02-11T18:17:53.086Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:04:54.617Z
---

# Existing movies
This plugin will scan through accepted entries, and reject any movie entry that is already found on disk.

## Syntax
```
exists_movie:
  path: /path/to/movies
  [type]: {dirs|files}
  [allow_different_qualities]: {better|yes|no}
  [lookup]: {imdb|no}
  [recursive]: {yes|no}
```


### Example
```yaml
exists_movie: /storage/movies/
```

### Example
```yaml
exists_movie:
  - /storage/movies-sd/
  - /storage/movies-hd/
```

## Advanced
### type
By default, exists_movie will scan for directories within the given folder(s). If you would like to scan for files instead, use:

```yaml
exists_movie:
  path: /storage/movies
  type: files
```

### allow_different_qualities
By default, the exists_movie will not allow downloading of different qualities of the same movie. (If you already have `Movie.720p` then `Movie.1080p` will be rejected.) If you would like to allow different qualities of the same movie, you can use the advanced form of configuration, like so:

```yaml
exists_movie:
  path: /storage/movies
  allow_different_qualities: yes
```

If you would only like to allow qualities that are better than what is currently on disk, you can use this format:

```yaml
exists_movie:
  path: /storage/movies
  allow_different_qualities: better
```

### lookup
By default, exists_movie will use the internal movie parser. If you would like to use imdb_lookup instead, use:

```yaml
exists_movie:
  path: /storage/movies
  lookup: imdb
```

### recursive
By default, exists_movie doesn't look into subfolders, to change that behavior use:
```yaml
exists_movie:
  path: /storage/movies
  recursive: yes
```