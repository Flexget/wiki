= IMDb list =

This plugin creates an [wiki:Entry Entry] for each item in an IMDb list.

This plugin is useful for example when used in a task with the [wiki:Plugins/movie_queue movie_queue] plugin (in 'add' mode) to add movies from your IMDb watchlist to your movie queue.

This plugin is a [wiki:list_interface list_interface] plugin.

'''Notes:''' 

 * Like with other APIs used by !FlexGet the IMDb list is cached for 2 hours to avoid hammering.
 * List must be public.

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
list_match:
  - imdb_list:
      login: 123@abc.com
      password: flexget
      list: watchlist
download: /downloads/
}}}
For more information about list action go to the [wiki:list_interface list_interface] page.
