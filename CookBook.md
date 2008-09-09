= CookBook = 

Feel free to add your own recipes.

== Index ==

 * [wiki:CookBook#DownloadFlexGetReleases Download FlexGet releases]
 * [wiki:CookBook#DownloadHeroesComics Download Heroes Comics]
 * [wiki:CookBook#DownloadDVDRipsFromRlsLog Download DVDRips from RlsLog.net]


== Download !FlexGet Releases ==

{{{
flexget:
  html: http://download.flexget.com
  patterns:
    - flexget_\(r\d*\)
  download: ~/flexget/
  interval: 3 days
}}}

Execute !FlexGet once with parameters:

{{{
flexget.py --feed flexget --learn
}}}

This will learn all matches as already downloaded, thus avoids downloading old versions.


== Download Heroes Comics ==

Download all/new heroes comics from [http://nbc.com/Heroes nbc.com]

{{{
heroes:
  text:
    url: http://www.nbc.com/Heroes/js/novels.js
    entry:
      title: novelTitle = "(.*)"
      url: novelPrint = "(.*)"
    format:
      url: http://www.nbc.com%(url)s
  interval: 6 hours
  download: ~/heroes/

}}}

== Download DVDRips From !RlsLog ==

{{{
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