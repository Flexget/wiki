= Sync from an IMDb to a trakt.tv list =

This recipe will keep your trakt watchlist in sync with your imdb watchlist. It is a one way sync, so direct changes to your trakt list will be overwritten by the imdb watchlist. This example is adaptable to sync any imdb list to any trakt list.

{{{
tasks:
  imdb_to_trakt:  # This task adds all the movies in your imdb watchlist to your trakt watchlist
    imdb_list:
      user_id: urXXXXXXXX
      list: watchlist
    accept_all: yes
    trakt_add:
      api_key: xxxxxx
      username: myusername
      password: mypassword
      movies: watchlist
    disable_builtins: [seen]

  imdb_to_trakt_remove:  # This task removes anything in your trakt watchlist which is no longer in your imdb watchlist
    trakt_list:
      api_key: xxxxxx
      username: myusername
      password: mypassword
      movies: watchlist
    crossmatch:
      from:
        - imdb_list:
            user_id: urXXXXXXXX
            list: watchlist
      fields: [imdb_id]
      action: reject
    accept_all: yes
    trakt_remove:
      api_key: xxxxxx
      username: myusername
      password: mypassword
      list: watchlist
    disable_builtins: [seen]
}}}