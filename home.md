= Welcome to FlexGet Trac =

FlexGet is a software that main focus is to automate downloading content from various sources. 
Most common usage is downloading .torrent files from RSS-feeds, but you can use it to download 
latest podcasts as well.

FlexGet is completely modular and all features are actually plugins.

== How easy is it to use? ==

Easy configuration was top priority when designing application. However some basic knowledge 
about regular expression is usually needed for effective usage.

FlexGet uses YML in configuration files. 

Short example (config.yml):

{{{
feeds:
  rss: http://something.com/rss.xml
  patterns:
    - serie.name
  download: ~/series
}}}

This example would download all .torrent files matching regular expression {{{serie.name}}}.

== Modules ==

=== Inputs ===

[wiki:InputRSS RSS], [wiki:InputHtml Html], [wiki:InputCSV CSV], [wiki:InputRlsLog RlsLog]

=== Filters ===

[wiki:FilterPatterns Pattenrs], [wiki:FilterImdb Imdb], [wiki:FilterSeen Seen]

=== Download ===

[wiki:FilterSeen Download]

=== Modify ===

[wiki:ModifyRemoveTrackers Remove Trackers]
