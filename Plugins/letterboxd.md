= Letterboxd =

This plugin produces an [wiki:Entry entry] for each film in any public [http://letterboxd.com Letterboxd] list. These entries can then be added to the [wiki:movie_queue#AddingRemovingusingTasks movie_queue], used to initiate a search with [wiki:discover discover], or passed to any other [wiki:Plugins#Outputs output plugin]. Results are cached for two hours to avoid flooding the site.
 
== Configuration ==

||=**Paramaters**    =||==||=An asterisk (*) indicates that the parameter is required =||
||**username***       ||  ||Your or another user's Letterboxd username. ||
||**list***           ||  ||The name of a custom list, or one of the following built in lists: `watchlist`, `diary`, `likes`, `rated` or `watched`. ||
||**sort_by**         ||  ||Determines the order in which films in the list will be returned (see below). ||
||**max_results**     ||  ||An integer specifying the maximum number of films that will be returned from the list. ||
||                    ||  ||||
||||||=**sort_by options** =||
||name                ||  ||Sorted by film title, ascending alphabetically. ||
||added               ||  ||Sorted by the date the film was added to the list, from most to least recent. ||
||popularity          ||  ||Sorted in descending order of popularity among Letterboxd users. ||
||length-ascending    ||  ||Sorted by runtime, from shortest to longest. ||
||length-descending   ||  ||Sorted by runtime, from longest to shortest. ||
||rating-ascending    ||  ||Sorted by the average rating given by Letterboxd users, from lowest to highest. ||
||rating-descending   ||  ||Sorted by the average rating given by Letterboxd users, from highest to lowest. ||
||release-ascending   ||  ||Sorted by date of theatrical release, from least to most recent. ||
||release-descending  ||  ||Sorted by date of theatrical release, from most to least recent. ||

The **username** and **list** parameters should be entered exactly as they appear in the URL for the list. For example, to get films from a list at `http://letterboxd.com/some-user/list/some-users-list/`, the username would be `some-user` (not `Some User`), and the list would `some-users-list` (not `Some User's list`).

== Usage notes ==

The plugin can easily be used to queue up films from your Letterboxd watchlist to be downloaded by another task:

{{{
tasks:
  queue-letterboxd-watchlist:
    letterboxd:
      username: *****
      list: watchlist
    accept_all: yes
    movie_queue: add
}}}

In addition to `title`, `url`, `imdb_id`, `tmdb_id`, `movie_name` and `movie_year`, [wiki:Entry entries] created by the plugin are populated with a few site-specific fields:

||||||=**Entry fields** =||
||**letterboxd_list**   || ||The list that the entry was pulled from, in the format `list (username)`. ||
||**letterboxd_score**  || ||The average rating (out of 10) given to the film by Letterboxd users (included when available). ||
||**letterboxd_uscore** || ||The rating (out of 10) given to the film by the list owner (included for `diary` and `rated` lists). ||

You can of course [wiki:Plugins#Filters filter] against any of these fields. `letterboxd_list` may be useful where more than one input plugin (or [wiki:inputs more than one Letterboxd list]) is included in the task. `letterboxd_score` and `letterboxd_uscore` can used in conjunction with [wiki:if Python if statements], like so:

{{{
tasks:
  queue-well-reviewed-films:
    letterboxd:
      username: *****
      list: diary
    if:
      - 'letterboxd_uscore >= 8': accept
    movie_queue: add
}}}

When dealing with large lists, it may be worthwhile to feed entries to an intermediary plugin such as [wiki:trakt_add trakt_add]. There is [http://letterboxd.com/api-coming-soon/ no publicly available API for Letterboxd] as of yet, so the plugin works by combing through the HTML source code for each film's page on the site. This isn't particularly fast if you want to, say, use [wiki:crossmatch crossmatch] to reject films you've marked as seen on Letterboxd. In that case, you could have your config set up like this:

{{{
tasks:
  add-to-trakt:
    letterboxd:
      username: *****
      list: watched
      sort_by: added
      max_results: 20  # <--- Set depending on how often you run the task; high enough that it will catch all new entries,
    accept_all: yes    #      but low enough so as not to parse (much) more of the list than is necessary. 
    trakt_add:
      username: *****
      password: *****
      list: watched

  download-films:
    some_input_plugin:
    ...
    crossmatch:
      from:
        - trakt_list:
            username: *****
            password: *****
            list: watched
            type: movies
      fields:
        - imdb_id
      action: reject
      ...
}}}