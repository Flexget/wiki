---
title: queue_movies
description: 
published: true
date: 2022-09-18T05:10:34.472Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:10:31.892Z
---

# Queue Movies
[Includes/PluginReplacedArchived](/Includes/PluginReplacedArchived){.include}

This plugin is an output plugin that adds a movies to your [movie_queue](/Plugins/movie_queue) for each accepted entry in a task. This plugin alone is not useful. To accept the queued movies you will need a task with [movie_queue](/Plugins/movie_queue) in it.

With this you could for example queue all movies in your imdb watchlist by creating following task.

**Example:**

```
tasks:
  queue_from_imdb:
    imdb_list:
      username: myimdbuser
      password: mypass
      list: watchlist
    accept_all: yes
    queue_movies: yes
```

Or from RSS feed.

**Example:**

```
tasks:
  queue_from_foobar:
    rss: http://foobar.com/rss.xml # input
    accept_all: yes                # filter which accepts everything
    queue_movies: yes              # output entries to movie queue (with quality any)
```

These are not tasks in traditional FlexGet sense as they don't download anything. Instead they are more like utility tasks.

Queue movies will work best with entries containing imdb_id/url or tmdb, if they're not available it will try to get them on it's own. Relying on this will mean that some of the entries may not be added to the [movie_queue](/Plugins/movie_queue).

## Options
You can also specify options for items being added to the movie queue. Most people will not want to use this option. Instead, the [quality](/Plugins/quality) plugin should be used in your download task.

```
queue_movies:
  quality: 720p+ bluray
```

See [qualities](/Qualities) page for valid quality requirements.