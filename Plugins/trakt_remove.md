# Trakt Remove
<div class="alert alert-danger" role="alert">Deprecated and removed!
</div>

This plugin has been replaced with [list_remove](/Plugins/List/list_remove).

The below information is stored for archival purposes and cannot be used with FlexGet versions past 2.1.0

## Archived information

**`IMPORTANT:` Please see [trakt](/Plugins/trakt) on how to authorize Flexget to access your private Trakt.tv account.**

This plugin will remove movies, series or episodes from a [trakt.tv](http://trakt.tv) list.

This plugin can be added to any of your tasks that deal with movies/series, or it can be used with the [filesystem](/Plugins/filesystem) plugin to remove all your already acquired movies on trakt.tv from a specified list.

Please note that `account` is **required**.

**Configuration:**

```
trakt_remove:
  username: <trakt username>
  account: <flexget account name>
  list: <list name>
  type: [auto|shows|seasons|episodes|movies](/auto|shows|seasons|episodes|movies)
```

The `list` option can be one of the built in trakt lists, `collection`, `watched`, or `watchlist`, or the name of one of your custom trakt lists.

Setting the `type` option to anything but auto (the default) forces entries to be of a given item type or not be removed.