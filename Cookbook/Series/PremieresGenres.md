= Premieres with genre filtering =

{{{
presets:
  premieres:
    thetvdb_lookup: yes
    require_field: series_genres
    regexp:
      reject:
        - documentary: {from: series_genres}
        - talk show: {from: series_genres}
        - game show: {from: series_genres}
    series_premiere: yes     
}}}

Adding this preset to series feeds will download all premieres except if their genres are documentary, talk show or game show. This works only if the series data is already in the thetvdb when premiere is seen, not entirely sure if this is the case.

Uses plugins: [wiki:Plugins/thetvdb_lookup thetvdb_lookup], [wiki:Plugins/require_field require_field], [wiki:Plugins/regexp regepx],[wiki:Plugins/series_premiere series_premiere]
