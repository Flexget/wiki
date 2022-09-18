---
title: movie_list
description: 
published: true
date: 2022-09-18T05:25:05.652Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:25:02.950Z
---

# Movie List
> This is part of [managed list](/Plugins/List) plugin system.
{.is-success}

> To improve matching, make sure you have a lookup plugin enabled, eg. [imdb_lookup](/Plugins/imdb_lookup).
{.is-info}

Any entry containing field(s) `imdb_id`, `trakt_movie_id` or `tmdb_id` can be added to movie list for later matching. This allows user to maintain one or more movie queues.

## Schema

```text
movie_list: <name>
```

Or:

```text
movie_list: 
  list_name: <name>
  [strip_year]: <yes|no>
```

**Clarification**: By default, entries that are generated from `movie_list` include the movie year (if available) in the entry _title_. Using `strip_year` only affects how `movie_list` creates the entry _title_ and not how it stores it. In other words, this option is only relevant when using `movie_list` as an input, either by itself in a task or when using [discover](/Plugins/discover) plugin.

### Matching
When using `movie_list` with a filter like [list_match](/Plugins/List/list_match) for example, the identifiers take precedence in matching over title, meaning that if the movie has an identifier (eg. _imdb_id_) and an entry with that same identifier type and value is examined, that movie will be matched. Thus it's preferable to use a lookup plugin in the task, preferably, the same one(s) that was used to add movie to the list.
If matching by identifiers fail, then title is [parsed](/Plugins/parsing) and proceeded to try to match by `movie_name` and `movie_year` fields.

## Usage
As a [managed list](/Plugins/List) plugin it follows the same list actions, an quick example how to add entries into the list.

```yaml
# inputs
# filters
list_add: 
  - movie_list: list name
```

### Fill list

#### Easily from trakt
```yaml
trakt_list:
  username: traktusername
  list: watchlist
  type: movies 
accept_all: yes
list_add:
  - movie_list: movies
```

This will add all accepted entries to an `movie_list` with the name `movies`. It then later be used as an input itself. CLI tools will default to list name `movies` if nothing is given so that is convenient name if you only have one list, with multiple lists you probably want something more descriptive. This created `movies` list can then be used a base to filter on with other tasks. 

#### With multiple inputs

```yaml
trakt_list:
  username: traktusername
  list: watchlist
  type: movies 
imdb_list:
  login: email@123.com
  password: flexget
  list: watchlist
list_add:
  - movie_list: all my watchlists
```

### Download matches

```yaml
rss: http://example.com/feed.xml
quality: 720p
imdb_lookup: yes
list_match:
  from:
    - movie_list: movie list name
download: /path/to/download
```

[quality](/Plugins/quality) is used to weed out any unwanted qualities. [imdb_lookup](/Plugins/imdb_lookup) is required for entries to be matched with movie_list.

### With discover
```yaml
discover-movies:
  discover:
    what:
      - movie_list: movies
    from:
      - rarbg: <opts>
  quality: 720p
  imdb_lookup: yes
  list_match:
    from:
      - movie_list: movies
  download: /path/to/download
```

**Strip Year option**: It is sometimes required by some search plugin to remove the year for the movie title. If that's the case, the following config can be used:

```yaml
discover-movies:
  discover:
    what:
      - movie_list: 
          list_name: movies
          strip_year: yes
    from:
      - rarbg: <opts>
  quality: 720p
  imdb_lookup: yes
  list_match:
    from:
      - movie_list: movies
  download: /path/to/download
```

The [list_match](/Plugins/List/list_match) matches only the first item from the list by default. See its wiki for different options.

Plugin [seen](/Plugins/seen) needs to be disabled since all the titles that movie queue will emit were seen when they were added to the queue

## Movie list CLI

See [movie-list commandline](/CLI/movie-list) how to view and manage the list via commandline.


## Movie List API
`movie_list` plugin has full API support. See [API post](http://discuss.flexget.com/t/flexget-rest-api/) for details