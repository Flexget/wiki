# Emby list
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; This is part of [managed list](/Plugins/List) plugin system.
</div>

This plugin creates an [Entry](/Entry) for each movie/series/season/episode from emby's, watched list, favorites, libraries or playlists

This plugin is useful for example when used in a task with the [movie_list](/Plugins/List/movie_list) plugin to add movies from your trakt watchlist to your [movie_list](/Plugins/List/movie_list), or to control the series plugin using [configure_series](/Plugins/configure_series).  

## Plugin Settings
Currently the following settings are supported:

| Option| Description |
| --- | --- |
| **host** | The emby host, including `protocol` and `port` |
| **username** | The `username` of the user, should be provided with `password` or with a `apikey`. If a `apikey` is informed, the user can be any user in the server, if a `password` is informed, the login `username` plus `password` must match |
| **password** | The `password` to authenticate the `username`  |
| **apikey** | The apikey to use to authenticate |
| **return_host** | What type of host to return in the url's, if `lan` or `wan`|
| **list** | The list to return, can be `watched`, `favorite`, a library, or a playlist. If typed, `watched` or `favorite`, those lists will be assumed, if it's a valid library, that will be assumed, if not, it will be assumed a playlist and created if it does not exist.

## Config format
```text
emby_list:
    server:
        host: http://localhost:8096
        username: <username>
        [apikey]: <apikey>
        [password]: <password>
        [return_host]: <wan|lan>
    list: <watched|favorite|library name|playlist name>
```

## Examples
### Add to Favorites

```yaml
list_add:
  - emby_list:
      server:
        host: http://emby.localhost:8096
        username: flexget
        password: flexget
        return_host: wan
      list: favorite
```

For more information about list action go to the [managed list](/Plugins/List) page.