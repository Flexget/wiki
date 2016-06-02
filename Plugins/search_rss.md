= Seach RSS =

A generic search plugin that can use rss based search feeds. Configure it like rss
plugin, but include {{search_term}} in the url where the search term should go.

'''Example:'''

{{{
discover:
  what: 
    - movie_list: movies
  from:
    - search_rss: http://domain.org&q={{ search_term }}
}}}