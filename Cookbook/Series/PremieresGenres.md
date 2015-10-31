= Premieres with genre filtering =

{{{
tasks:
   get_shows:
      rss: https://www.xxxx.com/feeds.php?xxxx
      series_premiere: yes
      thetvdb_lookup: yes
      require_field: tvdb_genres
      regexp:
        reject:
          - documentary: {from: tvdb_genres}
          - talk show: {from: tvdb_genres}
          - game show: {from: tvdb_genres}
}}}

Adding this template to series feeds will download all premieres except if their genres are documentary, talk show or game show. This works only if the series data is already in the thetvdb when premiere is seen, not entirely sure if this is the case.

Uses plugins: [wiki:Plugins/thetvdb_lookup thetvdb_lookup], [wiki:Plugins/require_field require_field], [wiki:Plugins/regexp regepx],[wiki:Plugins/series_premiere series_premiere]
