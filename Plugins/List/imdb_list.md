---
title: imdb_list
description: 
published: true
date: 2022-09-18T05:25:06.944Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:24:31.772Z
---

# IMDb list
> This is part of [managed list](/Plugins/List) plugin system.
{.is-success}

> IMDb enforces captchas more often than not, which the plugin currently cannot handle. If login fails, please open an issue on [Github](https://www.github.com/Flexget/Flexget/issues). If you do not need to alter IMDb lists, you can use [imdb_watchlist](/Plugins/imdb_watchlist) instead.
{.is-warning}

Creates an [Entry](/Entry) for each item in an IMDb list.

This plugin is useful for example when used in a task with the [movie_list](/Plugins/List/movie_list) plugin to add movies from your IMDb watchlist to your movie list, or to filter entries directly against the watchlist via [list_match](/Plugins/List/list_match) (see example below).

**Notes:** 

 * In order to avoid IMDB lockout due to hammering, credentials are cached to DB on first successful login and are used with every call to the plugin after that. (Password itself is not saved, just the login, resolved user ID and generated cookies)
 * When matching against the list, it will skip any entry that does not have an `imdb_id`, so using `imdb_lookup: yes` is advised.

## Cookies

In order to login into imdb we have to rely on browser cookies. You can get the cookie information from your browser. The required fields are:

* ubid-main
* at-main

**Get Cookie from Chrome:**

* Click the tree top right dots
* More Tools > Developer Tools
* Go to the Application tab, and on the left side select Cookies > https://www.imdb.com/
* Copy the content of ubid-main and sess-at-main into cookie

Cookies can be added to the config in several ways:

**Set Cookie in config:**

```yaml
imdb_list:
  login: my_login
  cookies:
    ubid-main: "<<from cookie>>"
    at-main: "<<from cookie>>"
  list: watchlist
```

**Set Cookie with [variables](/Plugins/variables):**

variables.yaml:

```yaml
imdb:
  login: mylogin@mail.com
  cookies:
    ubid-main: "xxx-xxxxxxxx-xxxxxxx"
    at-main: "XxXxXxXxXxXxXxXxXx"
  list: 'mylist'
```

config.yaml:

```yaml
imdb_list:
  login: '{? imdb.login ?}'
  cookies: '{? imdb.cookie ?}'
  list: '{? imdb.list ?}'
```

**Set Cookie in json format:**

```yaml
imdb_list:
  login: '{? imdb.login ?}'
  cookies: '{"ubid-main":"xxx-xxxxxxxx-xxxxxxx","at-main":"XxXxXxXxXxXxXxXxXx"}'
  list: '{? imdb.list ?}'
```

**Set Cookie from a file in JSON format:**

```yaml
imdb_list:
  login: '{? imdb.login ?}'
  cookies: '/path/to/file.json'
  list: '{? imdb.list ?}'
```

file.json

```yaml
{"ubid-main":"xxx-xxxxxxxx-xxxxxxx","at-main":"XxXxXxXxXxXxXxXxXx"}
```

## Example

```yaml
imdb_list:
  login: 123@abc.com
  cookies:
    ubid-main: "xxxxxxxxxxxx"
    at-main: "xxxxxxxxxx"
  list: watchlist
  force_language: es-mx # Optional - Force Specified Language
```

You can force a returned language using the `force_language` parameter. A list of valid language values can be found here [here](http://www.science.co.il/Language/Locale-codes.asp), You will need to select the proper **LCID language string**.


**List Action Example**

```yaml
rss: http://rss.com
imdb_lookup: yes
list_match:
  from:
    - imdb_list:
        login: 123@abc.com
        cookies:
          ubid-main: "xxxxxxxxxxxx"
          at-main: "xxxxxxxxxx"
        list: watchlist
download: /downloads/
```
