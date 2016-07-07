### List Remove
This plugin is a [list_interface](/Plugins/List/) plugin.

List plugins can have entries removed from them by using the `list_remove` plugin:
```
trakt_list:
  username: traktusername
  list: watchlist
  type: movies
accept_all: yes
list_remove:
  - trakt_list:
      username: a_different_username
      account: traktusername # required if list is not public
      list: watchlist
      type: movies
```