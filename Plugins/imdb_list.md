= IMDb list =

This plugin creates an [wiki:Entry Entry] for each item in an IMDb list.

This plugin is useful for example when used in a task with the [wiki:Plugins/movie_queue movie_queue] plugin (in 'add' mode) to add movies from your IMDb watchlist to your movie queue.

'''Notes:''' 

 * Like with other APIs used by !FlexGet the IMDb list is cached for 2 hours to avoid hammering.
 * List must be public.

'''Example:'''

{{{
imdb_list:
  user_id: ur9999999
  list: watchlist
  force_language: es-mx # Optional - Force Specified Language
}}}

Your user id can be found [http://www.imdb.com/list/watchlist here] when you are logged in.[[BR]]
You can force a returned language using the `force_language` parameter. A list of valid language values can be found here [http://www.science.co.il/Language/Locale-codes.asp here], You will need to select the proper '''LCID language string'''.

'''{{{WARNING:}}}''' If you are using a list other than the 'watchlist', 'ratings' or 'checkins', you currently have to look up the list id from imdb and use that instead of the name. This problem is being tracked in ticket #1303

'''Note:''' Adding this to your movie tasks or preset will NOT cause movies in imdb's watchlist to be accepted since this is an input, not a filter.