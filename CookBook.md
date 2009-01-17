= CookBook = 

Feel free to add your own recipes.

== Index ==

 * [wiki:CookBook#DownloadFlexGetReleases Download FlexGet releases]
 * [wiki:CookBook#DownloadDVDRipsFromRlsLog Download DVDRips from RlsLog.net]
 * [wiki:CookBook#DownloadHeroesComics Download Heroes Comics]
 * [wiki:CookBook#GenerateRSS Generate RSS feed for other clients]


== Download !FlexGet Releases ==

{{{
feeds:
  flexget:
    interval: 3 days
    html: http://download.flexget.com/0.9/
    patterns:
      - flexget
    download: ~/flexget/
}}}

Execute !FlexGet once with parameters:

{{{
flexget.py --feed flexget --learn
}}}

This will learn all matches as already downloaded, thus avoids downloading old versions.

Uses: [wiki:ModuleInterval interval], [wiki:InputHtml html], [wiki:FilterPatterns patterns], [wiki:OutputDownload download]

== Download DVDRips From !RlsLog ==

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

Uses: [wiki:InputRlsLog rlslog], [wiki:FilterImdb imdb], [wiki:OutputDownload download]

== Download Heroes Comics ==

Download all/new heroes comics from [http://nbc.com/Heroes nbc.com]. This uses advanced text-parsing module and does not represent accurately average usage.

{{{
feeds:
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

Uses: [wiki:ModuleInterval interval], [wiki:InputText text], [wiki:OutputDownload download]

== Generate RSS ==

This will produce rss-feed containing all matches with direct download urls (resolved). This is useful if you wish to hook up !FlexGet with a client that does not have a [wiki:WatchDirectory watch directory] support, or if you wish to perform downloading in a another computer. Only downside is that you need a HTTP server like Apache to host the RSS-feed.

{{{
global:
  make_rss:
    link: url
    file: ~/public_html/flexget.rss

feeds:
  some feed:
    patterns:
      - example

  another feed:
    series:
      - some serie
}}}

Uses: [wiki:GlobalSection global section], [wiki:OutputRSS make_rss]


== Series example ==

{{{
feeds:
  feed_example1:
    rss: http://example.com/torrents.xml
    series:
      - series name
      - another series
    download: ~/series

  feed_example2:
    rss: http://foo.com/torrents.xml
    series:
      - third series
      - fourth series
    download: ~/series
}}}