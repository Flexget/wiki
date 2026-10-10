---
title: floppy_list
description: 
published: true
date: 2026-10-04T00:00:00.000Z
tags: 
editor: markdown
dateCreated: 2026-10-04T00:00:00.000Z
---

# Floppy list
> This is part of [managed list](/Plugins/List) plugin system.
{.is-success}

This plugin creates an [Entry](/Entry) for each movie, show, season or episode in a list on a [Floppy](https://github.com/dannyvfilms/Floppy) server, a self-hosted media tracker. It can also add entries to and remove entries from those lists, including Floppy's collection of owned media.

This plugin is useful for example to download everything you put on a "to download" list in Floppy, and to mark what FlexGet downloaded as collected in Floppy.

>Floppy identifies movies and shows by their TMDB id. To add or remove an entry, the plugin uses the entry's `tmdb_id`. If that is missing it looks the TMDB id up from `tvdb_id` or `imdb_id`, and as a last resort searches TMDB for `movie_name` and `movie_year`, or for `series_name`. A search by name can pick the wrong title when several share a name, so prefer entries that carry an id, for example from [tmdb_lookup](/Plugins/tmdb_lookup) or [imdb_lookup](/Plugins/imdb_lookup). Including the year in the series name, like `Doctor Who (2005)`, also narrows the search.
{.is-warning}

**Notes:**

 * Like with other APIs used by FlexGet the Floppy list is cached for 2 hours when used as an input.
 * Adding this plugin to your tasks as an input will **not** cause the listed movies or series to be accepted since this is an input, not a filter.
 * `list` is the name of the list as shown in Floppy. It is not case sensitive. The list must already exist, the plugin does not create it.
 * Create the `api_key` in Floppy under **Settings → Integrations → App tokens**. It needs the `lists:read` and `lists:write` permissions for lists, and `watchlist:read` and `watchlist:write` for the collection.

## Plugin Settings
Currently the following settings are supported:

| Option| Description |
| --- | --- |
| **base_url** | Address of the Floppy server, for example `http://localhost:8000`. |
| **api_key** | A Floppy app token, or the account token. |
| **list** | Name of a Floppy list, or `collection` for the media you own. |
| **type** | Type of items to use, one of: `movies`, `shows`, `seasons`, `episodes` or `auto`. Default is `auto`, which uses every item in the list. |
| **strip_dates** | If set to `yes` the year will not be added to the end of titles. Default is `no`. |

## Config format
```text
floppy_list:
  base_url: <address of the floppy server>
  api_key: <floppy token>
  list: <list name|collection>
  [type]: <movies|shows|seasons|episodes|auto>
  [strip_dates]: <yes|no>
```

## What can be stored where

| | Movies | Shows | Seasons | Episodes |
| --- | --- | --- | --- | --- |
| **A Floppy list** | yes | yes | yes | no |
| **`collection`** | yes | no | no | yes |

When `type` is `auto`, the plugin submits the most specific thing an entry describes: an entry with `series_season` and `series_episode` is an episode, one with only `series_season` is a season, any other entry with `series_name` is a show, and everything else is a movie. An entry the target cannot hold is skipped with a warning.

To add or remove the show (or season) that an episode entry belongs to, set `type` to `shows` (or `seasons`).

Movies and episodes added to `collection` are stored with the resolution of the entry (for example `1080p`). Adding the same movie or episode again updates the resolution instead of creating a second copy.

## Entry fields

| Item | Fields |
| --- | --- |
| Movie | `title`, `url`, `movie_name`, `movie_year`, `tmdb_id`, `imdb_id` |
| Show | `title`, `url`, `series_name`, `tmdb_id`, `tvdb_id`, `imdb_id` |
| Season | `title`, `url`, `series_name`, `series_season`, `tmdb_id` |
| Episode | `title`, `url`, `series_name`, `series_season`, `series_episode`, `series_id`, `tmdb_id` |

Fields Floppy has no value for are left out. For seasons and episodes, `tmdb_id` is the id of the show.

## Matching
[list_match](/Plugins/List/list_match) and the other list actions compare an entry with the items of the list by `tmdb_id`, `tvdb_id` or `imdb_id`. If no id matches, movies are compared by `movie_name` and `movie_year`, and shows by `series_name`.

An item matches as what it is. A show in the list matches every episode of that show, and a season matches every episode of that season. An episode in the list, such as one in `collection`, only matches that same episode. Movies and series entries never match each other.

## Examples
### Download movies from a Floppy list
This example adds all the movies from a Floppy list called "To Download" to a [movie list](/Plugins/List/movie_list). This example should be in its own task, not combined with your movie downloading task.

```yaml
floppy_list:
  base_url: http://localhost:8000
  api_key: flp_xxxxxxxx
  list: To Download
  type: movies
accept_all: yes
list_add:
  - movie_list: listname
```

### Autoconfigure series
This example shows how the floppy_list plugin can be used with the [configure_series](/Plugins/configure_series) plugin in order to download all of the series in a Floppy list called "Following".

```yaml
configure_series:
  from:
    floppy_list:
      base_url: http://localhost:8000
      api_key: flp_xxxxxxxx
      list: Following
      type: shows
  settings:
    quality: 720p
```

### Mark downloads as collected
This marks every accepted movie and episode as owned in Floppy. In Floppy you can then filter your library by collected and not collected.

```yaml
tmdb_lookup: yes
list_add:
  - floppy_list:
      base_url: http://localhost:8000
      api_key: flp_xxxxxxxx
      list: collection
```

### Skip what you already own
This rejects movies and episodes that are already in your Floppy collection.

```yaml
list_match:
  from:
    - floppy_list:
        base_url: http://localhost:8000
        api_key: flp_xxxxxxxx
        list: collection
  action: reject
  remove_on_match: no
```

### Remove a movie from a list once it is downloaded
```yaml
tmdb_lookup: yes
list_remove:
  - floppy_list:
      base_url: http://localhost:8000
      api_key: flp_xxxxxxxx
      list: To Download
      type: movies
```

### Avoid repeating the server details
Use a YAML anchor, or a [template](/Plugins/template), to write the connection settings once.

```yaml
templates:
  floppy:
    list_add:
      - floppy_list: &floppy
          base_url: http://localhost:8000
          api_key: flp_xxxxxxxx
          list: collection

tasks:
  movies:
    template: floppy
    list_remove:
      - floppy_list:
          <<: *floppy
          list: To Download
          type: movies
```

For more information about list action go to the [managed list](/Plugins/List) page.
