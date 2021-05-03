# Emby Input
This plugin creates an [Entry](/Entry) for each movie/series/season/episode from emby's, watched list, favorites, libraries or playlists and filter based on some criteria

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
| **types** | What to return, `movies`, `series`, `season`, `episode`
| **watched** | Watched status `yes` or `no`|
| **favorite** | Favorite status `yes` or `no`|
| **sort** | Sort by `comunity_rating`, `critic_rating`, `date_created`, `date_played`, `play_count`, `premiere_date`, `production_year`, `sort_name`, `random`, `revenue`, `runtime`. Can also specify the order type in `field` and the `order` as  `ascending ` or  `descending `

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
    [watched]: <yes|no>
    [favorite] <yes|no>
    [sort]:
      field: <comunity_rating|comunity_rating|critic_rating|date_created|date_played|play_count|premiere_date|production_year|sort_name|random|revenue>
      [order]: <ascending|descending>
```

## Examples
### List Favorites

```yaml
from_emby:
  server:
    host: http://emby.localhost:8096
    username: flexget
    password: flexget
    return_host: wan
  list: favorite
  sort:
    field: random
    order: descending
    
from_emby:
  server:
    host: http://emby.localhost:8096
    username: flexget
    password: flexget
    return_host: wan
  list: favorite
  sort: premiere_date
```