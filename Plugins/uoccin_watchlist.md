---
title: uoccin_watchlist
description: 
published: true
date: 2022-09-18T05:16:14.629Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:16:11.956Z
---

# Uoccin watchlist add/remove
The `uoccin_watchlist_add` plugin adds the accepted movies and/or episodes in the watchlist inside your local uoccin.json file and update the [Uoccin](https://play.google.com/store/apps/details?id=net.ggelardi.uoccin) Android app database (if you are using it). The [uoccin_emit](/uoccin_emit) plugin can be used to produce titles from the watchlist in combination with other plugins like [configure_series](/configure_series) or [discover](/discover).

The `uoccin_watchlist_remove` remove the title from the movies or series watchlist.

## Plugin Settings
The following settings are supported:



|  Option  |  Description  |
| --- | --- |
| **uuid** | The machine identifier. Must be a simple but unique name, different for any device synchronizing on the same Google Drive account (i.e. "flexget_server", "home_pc1" etc). |
| **path** | This is the path to the uoccin.json file. |


### Example:
This example shows how the uoccin_watchlist_add plugin could be used to add series in the watchlist.

```
get_premieres:
    thetvdb_lookup: yes
    uoccin_lookup: path_to_uoccin_folder
    inputs:
      - rss: some_rss_feed
    series_premiere: yes
    require_field:
      - tvdb_genres
    if:
      - uoccin_tags or uoccin_watchlist or uoccin_watched or uoccin_collected: reject
      - 'reality' in tvdb_genres: reject
    uoccin_watchlist_add:
      uuid: this_machine_uuid
      path: path_to_uoccin_folder
```
  
**`IMPORTANT:`** The Android app can only be synchronized via Google Drive, so your uoccin.json file will reside in a folder named "uoccin" inside the root of your Google Drive folder.