= IMDb list =

This plugin is a [wiki:Plugins/List list_interface] plugin.

Creates an [wiki:Entry Entry] for each item in an IMDb list.

This plugin is useful for example when used in a task with the [wiki:Plugins/List/movie_list movie_list] plugin to add movies from your IMDb watchlist to your movie list, or to filter entries directly against the watchlist via `list_accept` (see example below).

'''Notes:''' 

 * In order to avoid IMDB lockout due to hammering, credentials are cached to DB on first successful login and are used with every call to the plugin after that. (Password itself is not saved, just the login, resolved user ID and generated cookies)
 * When matching against the list, it will skip any entry that does not have an `imdb_id`, so using `imdb_lookup: yes` is advised.

'''Example:'''

{{{
imdb_list:
  login: 123@abc.com
  password: flexget
  list: watchlist
  force_language: es-mx # Optional - Force Specified Language
}}}

You can force a returned language using the `force_language` parameter. A list of valid language values can be found here [http://www.science.co.il/Language/Locale-codes.asp here], You will need to select the proper '''LCID language string'''.


'''List Action Example'''
{{{
rss: http://rss.com
imdb_lookup: yes
list_accept:
  - imdb_list:
      login: 123@abc.com
      password: flexget
      list: watchlist
download: /downloads/
}}}
