# Trakt list
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; This is part of [managed list](/Plugins/List) plugin system.
</div>

This plugin creates an [Entry](/Entry) for each movie/show in one of the available [trakt.tv](http://trakt.tv) lists.

This plugin is useful for example when used in a task with the [movie_list](/Plugins/List/movie_list) plugin to add movies from your trakt watchlist to your [movie_list](/Plugins/List/movie_list), or to control the series plugin using [configure_series](/Plugins/configure_series).  


<div class="alert alert-warning" role="alert">

Trakt removes shows from watchlist if you watch them, so **do not** use watchlist as your primary series source, use a 
[custom list](http://support.trakt.tv/knowledgebase/articles/154739-why-do-things-get-removed-from-my-watchlist-after-) instead!
</div>

<div class="alert alert-info" role="alert">

Please see [Trakt Authentication](/Trakt_Authentication) for how to authorize FlexGet to access your Trakt.tv account.
</div>

**Notes:** 

 * Like with other APIs used by FlexGet the trakt.tv list is cached for 2 hours to avoid hammering.
 * Adding this plugin to your movie tasks or preset will **not** cause movies or series in the trakt list to be accepted since this is an input, not an filter.
 * If your trakt lists are not publicly available, you will need to authorize your account via the `flexget trakt auth` CLI command, then specify the **account** in your trakt configuration.
 * **If you wish to modify a trakt list from FlexGet eg. adding to/removing from a list, you must specify `account`**
 * If you want HTML-formatted lists, ex: "<b>TV Shows:</b> Get", to use that list, enter the list on trakt.tv and copy the part of the url that mentions it (ex: "b-tv-shows-b-get"). Basically, the displayed list name is **not** the same as the URL-friendly name, and trakt_list wants the URL-friendly name!

## Plugin Settings
Currently the following settings are supported:

| Option| Description |
| --- | --- |
| **username** | This is the username at [trakt.tv](http://trakt.tv) which owns the list. If `account` is specified, this will default to the owner of said account. |
| **account** | This is **required** if the profile is protected or to get private custom lists or manipulating lists eg. adding a movie to the list. It should be created via the `flexget trakt auth` CLI command. |
| **strip_dates** | If set to `yes` the year will be removed from the end of titles that contain them. |
| **list** |Name of a custom trakt list, or one of the built in ones: `watchlist`, `collection`, `watched`, `popular`, or `trending` |
| **type** | Type of items to be listed, can be one of: `movies`, `shows`, or `episodes`|
| **limit** | Maximum amount of produced items; especially useful for `trending` and `popular` lists |

## Config format
```text
trakt_list:
  username: <trakt username>
  [account]: <account set up in CLI>
  [strip_dates]: <yes|no>
  [limit]: <integer>
  list: <list name>
  type: <movies|shows|episodes>
```

## Examples
### Queue movies
This example shows how you would use trakt_list plugin with [movie_list](/Plugins/List/movie_list), in order to add all the movies from your trakt watchlist to your [movie list](/Plugins/List/movie_list). This example should be in its own task, not combined with your movie downloading task.

```yaml
trakt_list:
  username: traktusername
  account: traktusername # required if list is not public
  list: watchlist
  type: movies
accept_all: yes
list_add:
  - movie_list: listname
```

### Autoconfigure series
This example shows how the trakt_list plugin can be used with the [configure_series](/Plugins/configure_series) plugin in order to download all of the series you have included in a custom trakt list called 'following shows'.

```yaml
configure_series:
  from:
    trakt_list:
      username: traktusername
      account: traktusername # required if list is not public
      list: following shows
      type: shows
  settings:
    quality: 720p
```

### List action example
This would move items from account to another.
```yaml
trakt_list:
  username: traktusername
  list: watchlist
  type: movies
accept_all: yes
list_add:
  - trakt_list:
      account: a_different_username
      username: a_different_username
      list: watchlist
      type: movies
```

For more information about list action go to the [managed list](/Plugins/List) page.