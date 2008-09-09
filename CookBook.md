= CookBook = 

Feel free to add your own recipes.

== Index ==

 * [wiki:CookBook#DownloadFlexGetReleases Download FlexGet releases]
 * [wiki:CookBook#DownloadHeroesComics Download Heroes Comics]
 * [wiki:CookBook#DownloadDVDRipsFromRlsLog Download DVDRips from RlsLog.net]


== Download !FlexGet Releases ==

{{{
flexget:
  interval: 3 days
  html: http://download.flexget.com
  patterns:
    - flexget_\(r\d*\)
  download: ~/flexget/
}}}

Execute !FlexGet once with parameters:

{{{
flexget.py --feed flexget --learn
}}}

This will learn all matches as already downloaded, thus avoids downloading old versions.

Uses: [wiki:ModuleInterval interval], [wiki:InputHtml html], [wiki:FilterPatterns patterns], [wiki:OutputDownload download]

== Download Heroes Comics ==

Download all/new heroes comics from [http://nbc.com/Heroes nbc.com]

{{{
heroes:
  interval: 6 hours
  text:
    url: http://www.nbc.com/Heroes/js/novels.js
    entry:
      title: novelTitle = "(.*)"
      url: novelPrint = "(.*)"
    format:
      url: http://www.nbc.com%(url)s
  download: ~/heroes/

}}}

Uses: [wiki:ModuleInterval interval], [wiki:InputText text], wiki:OutputDownload download]

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

Uses: [wiki:InputRlsLog rlslog], [wiki:FilterImdb imdb], [wiki:OutputDownload download]