= Html =

Parses urls from html page. Usefull on sites which have direct download
links of any type (mp3, jpg, torrent, ...).

Many anime-fansubbers do not provide RSS-feed, this works well in many cases.

=== Example ===

{{{
html: <url>
}}}

Note: This returns ALL links from the page so you need to configure some filters to match only to desired content.

=== Example with regexp ===

{{{
html: <url>
regexp:
  accept:
    - podcast.*\.mp3
  rest: filter
}}}

This would download all links that have mp3 link with word podcast in them.

== Advanced ==

You can dump the received HTML into a file by using parameter {{{dump}}}.

=== Example ===

{{{
html:
  url: <url>
  dump: file.html
}}}

Some feeds contain links that have useless title (like 'DL'). If you need better titles you can use option {{{title_from_url}}} to guess better title from url.

=== Example ===

{{{
html:
  url: <url>
  url_from_title: true
}}}