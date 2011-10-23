= Upload movie/tv collection to trakt.tv =
These feeds will upload your collection to [http://trakt.tv trakt.tv].

Upload movie collection to [http://trakt.tv trakt.tv].
This is likely to generate errors and not work 100%. This is because of issues with other modules. Most of my  issues came from a unicode module not handling high order characters and the imdb plugin not matching all titles.

{{{
presets:
  global:
    # Setup defaults for trakt.tv collection updates
    find:
      # Regex to match all video with these extensions in your collection
      regexp: '.*\.(avi|mkv|mp4)$'
      recursive: yes
    accept_all: yes
    trakt_acquired:
      username: myusername
      password: mypassword
      api_key: myapikey

  update-movies:
    find:
      path:
        # All the paths where you store movies
        - /share/Video/Anime
        - /share/Video/Anime Collections
        - /share/Video/Movie Collections
        - /share/Video/Movies
        - /share/Video/Movies to Watch
    imdb_lookup: yes
    trakt_acquired:
      type: movies
    queue_movies: yes
    movie_queue:  yes

feeds:
  Update-Movies:
    preset:
      - global
      - update-movies
}}}

Upload TV collection to [http://trakt.tv trakt.tv].
This does not work yet. Still figuring out how to get the upload to trigger.
{{{
  update-tv:
    find:
      path:
        # All the paths where you store TV episodes
        - /mnt/NMVideo/TV
        - /mnt/NMVideo/TV Anime
        - /mnt/NMVideo/TV Food
    trakt_acquired:
      type: series

feeds:
  Update-TV:
    preset:
      - global
      - update-tv
}}}

Plugins used: [wiki:Plugins/accept_all accept_all], [wiki:Plugins/find find], [wiki:Plugins/imdb_lookup imdb_lookup], [wiki:Plugins/movie_queue movie_queue], [wiki:Plugins/preset preset], [wiki:Plugins/queue_movies queue_movies], [wiki:Plugins/trakt_acquired trakt_acquired], 
