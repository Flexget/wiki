= Upload movie/tv collection to trakt.tv =

These feeds will upload your collection to [http://trakt.tv trakt.tv].

Upload movie collection to [http://trakt.tv trakt.tv].
This is likely to generate errors and not work 100%. This is because of issues with other plugins. Most of my issues came from a unicode module not handling high order characters and the imdb plugin not matching all titles.

I would recommend making this a separate configuration file which you manually run only once or when needed. You can set up tract_acquired updating to your normal configuration file. If you put these into your config that is ran by cron, specify [wiki:Plugins/interval interval] for update feeds. Something along once per day or week.

{{{
tasks:

  Update-TV:
    filesystem:
      # Regex to match all video with these extensions in your collection
      regexp: '.*\.(avi|mkv|mp4)$'
      recursive: yes
      path:
        # All the paths where you store TV episodes
        - /mnt/NMVideo/TV
        - /mnt/NMVideo/TV Anime
        - /mnt/NMVideo/TV Food
    metainfo_series: yes
    accept_all: yes
    trakt_acquired:
      username: myusername
      password: mypassword
      api_key: myapikey
      type: series

  Update-Movies:
    # For movies we use filesystem.
    filesystem:
      - /share/movies
    accept_all: yes
    imdb_lookup: yes
    trakt_acquired:
      username: myusername
      password: mypassword
      api_key: myapikey
      type: movies
}}}

Plugins used: [wiki:Plugins/filesystem filesystem], [wiki:Plugins/accept_all accept_all], [wiki:Plugins/metainfo_series metainfo_series], [wiki:Plugins/imdb_lookup imdb_lookup], [wiki:Plugins/template template], [wiki:Plugins/trakt_acquired trakt_acquired]
