---
title: best_quality
description: 
published: true
date: 2024-04-02T16:50:36.654Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:02:29.675Z
---

# Best Quality
The best_qality plugin will sort entries, grouped by an identifier, and allow action on the best quality and lower qualities. 

## Settings

| **Option** | **Default** | **Description** |
| --- | --- | --- |
| identified_by | auto | Define how entries are identified to be a same content, default value `auto` uses entry `media_id` [field](https://flexget.com/Entry). Supports [Jinja Template](https://flexget.com/Jinja). |
| on_best | do_nothing | The action to preform on which has the best quality. Value `do_nothing` won't act on the entry ([undecided](https://flexget.com/FilterOperations))  but allow it to by handled by other plugins. |
| on_lower | reject | The action to preform on entries which are lower then the best quality. Value `do_nothing` won't act on the entry ([undecided](https://flexget.com/FilterOperations))  but allows it to by handled by other plugins. |
| single_best | yes | Consider only the first one as the best entry. |


## Syntax:

```
best_quality:
  identified_by: <jinja template>
  on_best: [accept|reject|do_nothing]
  on_lower: [accept|reject|do_nothing]
  single_best: [yes|no]
```

### Example

Let's assume the input has several of the same movie. The best_quality plugin will only allow the best quality.

```yaml
tasks:
  high_rated_movies:
    best_quality:
      # Let imdb handle the accept
      on_best: do_nothing
      on_lower: reject
    imdb:
      min_score: 8.5
      min_votes: 5000
```

### Example with custom identifier

The [metainfo_series](https://flexget.com/Plugins/metainfo_series) and [metainfo_movie](https://flexget.com/Plugins/metainfo_movie) plugins will, by default, set an identifier.

You can override the format using [Jinja Templates](https://flexget.com/Jinja).

```yaml
best_quality:
  identified_by: "{{ some_identifying_field }}"
```

### Example with [timeframe](https://flexget.com/Plugins/timeframe) and [upgrade](https://flexget.com/Plugins/upgrade)

In this example the first task will download movies, waiting 1 day for 1080p. If 720p and 1080p of the same movie appears up in the feed at the same time best_quality will ensure only the best is accepted by imdb.

The second task will upgrade the movie in future for 1 week.

```yaml
tasks:
  great_movies:
    # any input works, using rss as an example
    rss: https://example.com/feed.xml
    upgrade:
      # We must add this so the upgrade plugin can track the downloaded qualities
      tracking: yes
    timeframe:
      wait: 1 day
      # Let imdb handle the accept
      on_reached: do_nothing
      target: 1080p
    # If input has same movie twice, ensure only best get's through.
    best_quality:
      on_best: do_nothing
      on_lower: reject
    imdb:
      min_score: 7.5
      min_votes: 5000
    # any output works, using download as an example
    download: ~/watchfolder/

  upgrade_movies:
    # any input works, using rss as an example
    rss: https://example.com/feed.xml
    upgrade:
      timeframe: 1 week
      target: 1080p
      propers: yes
    # any output works, using download as an example
    download: ~/watchfolder/
```
