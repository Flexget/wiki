---
title: anidb_list
description: 
published: true
date: 2022-09-18T05:25:06.944Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:01:58.841Z
---

# AniDB List

This plugin produces an [entry](/Entry) for each movie or series on a public [AniDB](http://www.anidb.net) wishlist. These entries can then be added to the [movie_list](/Plugins/List/movie_list), used to initiate a search with [discover](/discover), or passed to some other [output plugin](/Plugins#Outputs). Results are cached for two hours to avoid flooding the site.

**Notes:** 

 * Like with other APIs used by FlexGet the AniDB list is cached for 2 hours to avoid hammering.
 * Adding this plugin to your movie tasks or preset will NOT cause movies or series in the trakt list to be accepted since this is an input, not a filter.
 * You can find the **user_id** on their profile page. Their wishlist must be public.

## Configuration

| Option | Description |
| --- | --- |
| user_id | Your or another user's AniDB id.|
| type |Type of items to be listed, can be one of: `movies` or `shows` |
| strip_dates | If set to `yes` the year will be removed from the end of titles that contain them. |

## Examples

### Queue movies

The plugin can easily be used to queue up films from your AniDB wishlist to be downloaded by another task:

```yaml
anidb_list:
  user_id: anidbid
accept_all: yes
list_add:
  - movie_list: movies
```

### Autoconfigure series

This example shows how the `anidb_list` plugin could be used with the [configure_series](/Plugins/configure_series) plugin in order to download all of the series you have included in your wishlist.

```yaml
configure_series:
  from:
    anidb_list:
      user_id: anidbid
      type: shows
  settings:
    quality: 720p
```