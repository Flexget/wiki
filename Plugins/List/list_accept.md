=== List Accept ===
List plugins can be used as positive filters with the `list_accept` plugin:
{{{
rss: some_feed...
list_accept:
  - trakt_list:
      username: traktusername
      list: watchlist
      type: movies
download: /downloads/
}}}
This will accept any entries that match the entries contained within the list plugin. 
By default, any accepted entry will be removed from match list. This can be changed using the following schema:
{{{
rss: some_feed...
list_accept:
  lists:
    - trakt_list:
        username: traktusername
        list: watchlist
        type: movies
  remove_on_accept: no
download: /downloads/
}}}