= Download movies from !RlsLog =

Uses [http://imdb.com imdb] details to filter out "bad" movies. Customize to your likings.

{{{
feeds:
  rlslog_dvdrips:
    rlslog: http://www.rlslog.net/category/movies/dvdrip/
    imdb:
      min_score: 6.1
      min_votes: 5000
      min_year: 2006
      reject_genres:
        - horror
        - documentary
        - musical
        - music
        - biography
    download: ~/torrents/
}}}

Uses plugins: [wiki:Plugins/rlslog rlslog], [wiki:Plugins/imdb imdb], [wiki:Plugins/download download]