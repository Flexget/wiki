= Html =

Parses urls from html page. Usefull on sites which have direct download
links of any type (mp3, jpg, torrent, ...).

Many anime-fansubbers do not provide RSS-feed, this works well in many cases.

= Example =

{{{
html: <url>
}}}

Note: This returns ALL links on url so you need to configure [wiki:FilterPatterns patterns] filter
to match only to desired content.