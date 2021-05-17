# Managed List Plugins
Managed list plugins are a class of plugin which work as input plugins, but can also be used in other contexts to edit the list or act certain way based on the list content.

| Plugin name | Description |
| --- | --- |
| [trakt_list](/Plugins/List/trakt_list) | Use or add entries from one of your trakt.tv lists. |
| [imdb_list](/Plugins/List/imdb_list) | Use or add entries from one of your IMDB lists. |
| [couchpotato_list](/Plugins/List/couchpotato_list) | Use or add entries from one of your couchpotato watch list. |
| [sonarr_list](/Plugins/List/sonarr_list) | Use or add entries from Sonarr shows. |
| [radarr_list](/Plugins/List/radarr_list) | Use or add entries from Radarr. |
| [entry_list](/Plugins/List/entry_list) | Use or add entries to a custom made entry list. |
| [movie_list](/Plugins/List/movie_list) | Use or add entries to a custom made movie list. |
| [subtitle_list](/Plugins/List/subtitle_list) | Use or add entries to a custom made subtitle list. |
| [regexp_list](/Plugins/List/regexp_list) | Use or add entries to a custom made regexp list. |
| [thetvdb_list ](/Plugins/List/thetvdb_list) | Use or add entries from your TheTVDB favorites list. |
| [pending_list](/Plugins/List/pending_list) | Manually approve entries to be accepted
| [emby_list](https://flexget.com/Plugins/emby_list) | Allows list management in emby server

### Operating with lists


| Plugin name | Description |
| --- | --- |
| [list_add](/Plugins/List/list_add) | Use this plugin to add accepted entries to a list plugin. |
| [list_remove](/Plugins/List/list_remove) | Use this plugin to remove accepted entries from a list plugin. |
| [list_match ](/Plugins/List/list_match) | Use this plugin to filter entries based on the contents of a list. |
| [list_clear](/Plugins/List/list_clear) | Use this plugin to clear all items from a list plugin. |

## List action advanced usage
All of the aforementioned list plugins take a list of list plugin in their schema, so all operation can be used on multiple plugins at the same time:

```yaml
trakt_list:
  username: traktusername
  list: watchlist
  type: movies
accept_all: yes
list_add:
  - trakt_list:
      username: a_different_username
      list: watchlist
      type: movies
  - imdb_list:
      login: 'email@123.com'
      password: flexget
      list: watchlist
```

### Developers
Want to create or convert an existing plugin to a managed list plugin? [Read the docs](https://github.com/Flexget/Flexget/blob/develop/docs/develop/list_interface.rst).