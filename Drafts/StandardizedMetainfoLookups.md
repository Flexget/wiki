---
title: StandardizedMetainfoLookups
description: 
published: true
date: 2022-09-18T04:58:32.665Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:58:30.066Z
---

## Goals
- Have a standardized framework for metainfo providers, so that plugins which require metainfo aren't coupled so tightly to one specific metainfo provider.
- Let the user customize priority and which providers are allowed in the task.
- Allow requesting a metainfo lookup for a certain category (series, movies, etc.)

## Places that might use it
- generic metainfo lookup plugin to provide lazily looked up entry fields, perhaps used in a template, or by another plugin
- cli utilities, e.g. movie-queue cli command wants to look up a movie title to enqueue
- If an user has not specified an explicit metainfo lookup in task, plugins like imdb or movie_queue still want to access some of those fields

## Configuration
Suggested formats:

```
metainfo:
  type: series
  provider: trakt
```
----------------
Alternate idea: metainfo providers are configured at the root of the config. This way, even things like cli utilities (movie queue) can request a lookup which can use the users settings.
```
tasks:
  a:
    metainfo: series
# Optional customization of metainfo providers:
metainfo_providers:
  series:
    - trakt
  movies:
    - imdb
    - tmdb
```

### Questions
- Can a plugin request a specific field be looked up? Perhaps movie_queue wants to check the tmdb_id of an entry? What if the user has only specified imdb?
- Related: How do we handle lazy fields? If the framework doesn't know what fields each metainfo plugin provides beforehand, it can't register lazy fields.

*TODO: MORE*