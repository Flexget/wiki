= Upload movie/tv collection to trakt.tv =

These feeds will upload your collection to [http://trakt.tv trakt.tv].

Upload movie collection to [http://trakt.tv trakt.tv].
This is likely to generate errors and not work 100%. This is because of issues with other plugins. Most of my issues came from a unicode module not handling high order characters and the imdb plugin not matching all titles.

I would recommend making this a separate configuration file which you manually run only once or when needed. You can set up tract_acquired updating to your normal configuration file. If you put these into your config that is ran by cron, specify [wiki:Plugins/interval interval] for update feeds. Something along once per day or week.

{{{
presets:
  acquired:
    trakt_acquired:
      username: myusername
      password: mypassword
      api_key: myapikey

feeds:

  Update-TV:
    preset: [acquired]
    find:
      # Regex to match all video with these extensions in your collection
      regexp: '.*\.(avi|mkv|mp4)$'
      recursive: yes
      path:
        # All the paths where you store TV episodes
        - /mnt/NMVideo/TV
        - /mnt/NMVideo/TV Anime
        - /mnt/NMVideo/TV Food
    all_series: yes
    trakt_acquired:
      type: series

  Update-Movies:
    preset: [acquired]
    # For movies we use listdir instead of find since movies are (often) 
    # stored in directories and their names are generally much 
    # better than filenames.
    # You can use find plugin like with series if you need to.
    listdir:
      - /share/movies
    accept_all: yes
    imdb_lookup: yes
    trakt_acquired:
      type: movies
}}}

Plugins used: [wiki:Plugins/accept_all accept_all], [wiki:Plugins/all_series all_series], [wiki:Plugins/find find], [wiki:Plugins/imdb_lookup imdb_lookup], [wiki:Plugins/movie_queue movie_queue], [wiki:Plugins/preset preset], [wiki:Plugins/queue_movies queue_movies], [wiki:Plugins/trakt_acquired trakt_acquired], 
