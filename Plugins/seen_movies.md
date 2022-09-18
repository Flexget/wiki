---
title: seen_movies
description: 
published: true
date: 2022-09-18T05:12:29.231Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:12:26.668Z
---

# Filter Seen Movies
Prevents movies being downloaded twice.

How duplicate movie detection works:
 * Remembers all imdb, tmdb and trakt movie IDs from downloaded entries.
 * If stored ID appears again, entry is rejected.

## Configuration
### Matching
There are two different operating modes, `strict` and `loose`.

Strict mode will reject all entries that have not been identified as movies. Loose mode will not intervene.

```
seen_movies: strict
```
or
```
seen_movies:
  matching: strict
```

### Scope
By default this plugin will only allow a movie to be accepted once in any task. You can limit it to the current task by changing the scope to `local`.
```
seen_movies:
  scope: local
```