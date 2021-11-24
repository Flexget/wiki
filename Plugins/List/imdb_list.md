# IMDb list
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; This is part of [managed list](/Plugins/List) plugin system.
</div>

<div class="alert alert-warning" role="info">

  IMDb enforces captchas more often than not, which the plugin currently cannot handle. If login fails, please open an issue on [Github](https://www.github.com/Flexget/Flexget/issues). If you do not need to alter IMDb lists, you can use [imdb_watchlist](/Plugins/imdb_watchlist) instead.
</div>

Creates an [Entry](/Entry) for each item in an IMDb list.

This plugin is useful for example when used in a task with the [movie_list](/Plugins/List/movie_list) plugin to add movies from your IMDb watchlist to your movie list, or to filter entries directly against the watchlist via [list_match](/Plugins/List/list_match) (see example below).

**Notes:** 

 * In order to avoid IMDB lockout due to hammering, credentials are cached to DB on first successful login and are used with every call to the plugin after that. (Password itself is not saved, just the login, resolved user ID and generated cookies)
 * When matching against the list, it will skip any entry that does not have an `imdb_id`, so using `imdb_lookup: yes` is advised.

## Cookies

In order to login into imdb we now use cookies! You can get this cookies information from your browser and load the required fields into flexget. The required fields are:

* ubid-main
* sess-at-main

**Get Cookie from Chrome:**

* Click the tree top right dots
* More Tools > Developer Tools
* On the left side select Cookies > https://www.imdb.com/
* Copy the content of ubid-main and sess-at-main into cookie

```
imdb_list:
  login: my_login
  cookies:
    ubid-main: "<<from cookie>>"
    sess-at-main: "<<from cookie>>"
  list: watchlist
```

**Set Cookie with [variables](/Plugins/variables):**

variables.yaml:

```
imdb:
  login: mylogin@mail.com
  cookie:
    ubid-main: "xxx-xxxxxxxx-xxxxxxx"
    sess-at-main: "XxXxXxXxXxXxXxXxXx
  list: 'mylist'
```

config.yaml:

```
imdb_list:
  login: '{? imdb.login ?}'
  cookies: '{? imdb.cookie ?}'
  list: '{? imdb.list ?}'
```

## Example

```
imdb_list:
  login: 123@abc.com
  cookies:
    ubid-main: "xxxxxxxxxxxx"
    sess-at-main: "xxxxxxxxxx"
  list: watchlist
  force_language: es-mx # Optional - Force Specified Language
```

You can force a returned language using the `force_language` parameter. A list of valid language values can be found here [here](http://www.science.co.il/Language/Locale-codes.asp), You will need to select the proper **LCID language string**.


**List Action Example**
```
rss: http://rss.com
imdb_lookup: yes
list_match:
  from:
    - imdb_list:
        login: 123@abc.com
        cookies:
          ubid-main: "xxxxxxxxxxxx"
          sess-at-main: "xxxxxxxxxx"
        list: watchlist
download: /downloads/
```
