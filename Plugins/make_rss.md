= Output RSS =

Write RSS containing succeeded (downloaded) entries.

=== Example ===

{{{
make_rss: ~/public_html/flexget.rss
}}}

You may write into same file in multiple feeds.

=== Example ===

{{{
my-feed-A:
  make_rss: ~/public_html/series.rss
  .
  .
my-feed-B:
  make_rss: ~/public_html/series.rss
  .
  .
}}}

With this example file `series.rss` would contain succeeded
entries from both feeds.

Tip: use a global [wiki:Plugins/preset preset] to make RSS out of every feed without having to configure them individually.

=== Example ===

{{{
global:
  make_rss: ~/public_html/flexget.rss

feeds:
  my-feed-A:
    .
    .
  my-feed-B:
    .
    .
}}}


== Number of days / items ==
        
By default output contains items from last 7 days. You can specify
different perioid, number of items or both. Value -1 means unlimited.
        
=== Example ===
        
{{{
make_rss:
  file: ~/public_html/series.rss
  days: 2
  items: 10
}}}
          
Generate RSS that will containg last two days and no more than 10 items.
        
=== Example ===

{{{        
make_rss:
  file: ~/public_html/series.rss
  days: -1
  items: 50
}}}
          
Generate RSS that will contain last 50 items, regardless of dates.
        
== RSS link ==
        
You can specify what field from entry is used as a link in generated rss feed.
        
=== Example ===

{{{        
make_rss:
  file: ~/public_html/series.rss
  link:
    - imdb_url
}}}
            
List should contain a list of fields in order of preference.
Note that the url field is always used as last possible fallback
even without explicitly adding it into the list.
        
Default list: imdb_url, input_url, url

== Encoding ==

Since some clients do not support RSS properly (ahem, uTorrent). Starting from r1648 you can specify encoding.

=== Example ===

{{{
make_rss:
  file: ~/public_html/series.rss
  encoding: utf-8
}}}