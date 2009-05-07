[[PageOutline]]

= CookBook = 

{{{
#!html
<div id="login_note" style="width: 45em">Feel free to add your own recipes.<br> To edit wiki you need to login with username: <b>flexget</b> password: <b>anon</b></div>
}}}

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

If you wish to receive emails when updated version has been downloaded, add [wiki:OutputEmail email] plugin.

Uses plugins: [wiki:ModuleInterval interval], [wiki:InputHtml html], [wiki:FilterPatterns patterns], [wiki:OutputDownload download]

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

Uses plugins: [wiki:InputRlsLog rlslog], [wiki:FilterImdb imdb], [wiki:OutputDownload download]

== Download Heroes Comics ==

Download all/new heroes comics from [http://nbc.com/Heroes nbc.com]. This uses advanced text-parsing plugin and does not represent accurately average usage.

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

Uses plugins: [wiki:ModuleInterval interval], [wiki:InputText text], [wiki:OutputDownload download]

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

Uses plugins: [wiki:GlobalSection global section], [wiki:OutputRSS make_rss]

== Series - simple example ==

Just change feed names, rss urls and serie names :)

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

== Series - get only certain qualities ==

Regexp is used to reject all entries which do '''not''' have PDTV or HDTV in their information. ''This will be made easier in 1.0''

{{{
feeds:
  tvrss combined:
    rss: http://tvrss.net/feed/unique/
    regexp:
      reject_excluding: 
        - PDTV
        - HDTV
    series:
      - dollhouse
      - chuck
    download: ~/torrents
}}}

Uses plugins: [wiki:InputRSS RSS], [wiki:FilterSeries series], [wiki:FilterRegexp regexp], [wiki:OutputDownload download]

== Multiple feeds ==

{{{
feeds:
  tvrss combined:
    rss: http://tvrss.net/feed/unique/
    series:
      - south park
    download: ~/torrents

  vegapunk:
    rss: http://bt.vegapunk.com/rss/rss.xml
    patterns:
      - ^\[vegapunk\].*one.piece.*\d\d\d.HD
    download: ~/torrents

  baka:
    rss: 
      url: http://www.baka-updates.com/rss.php
      link: feedburner_origlink
      ascii: True
    regexp:
      accept:
        - SoulEaterFan.*Soul.Eater
        - ANBU.*Tytania.*HQ.*
      rest: filter
    download: ~/torrents
}}}

Uses plugins: [wiki:InputRSS RSS], [wiki:FilterPatterns patterns] (deprecated), [wiki:FilterSeries series], [wiki:FilterRegexp regexp], [wiki:OutputDownload download]


== Making single must have list ==

You can use global section and [wiki:FilterRegexp] to make a neat must-have list.

{{{
global:
  regexp:
    accept:
      - must have this
      - and that
      - and even this
feeds:
  .
  .
  .
}}}

Now these matches are downloaded regardless of the feed they occur in.

== Complete working example for rTorrent ==

There is also a complete example how to set up an [wiki:CookBook/rtorrent automatic downloader using rTorrent] and !FlexGet on a separate page
