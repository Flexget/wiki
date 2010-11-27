= Html =

Parses URLs from html page. Useful on sites which have direct download links of any type (mp3, jpg, torrent, ...).

Many anime-fansubbers do not provide an RSS-feed, this usually works for those cases.

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

== Title options ==

Some feeds contain links that have useless names (like 'DL', '1', '2'..). To get more useful titles use option {{{title_from}}}.

=== Example ===

{{{
html:
  url: <url>
  title_from: url
}}}

Other possible values are: `auto` ''(default)'', `url`, `title` and `link`. 

=== Example: url ===

If captured URL is "!http://some.domain.com/download/Podcast.2010-01-02.mp3" the extracted title would be "Podcast.2010-01-02.mp3"

=== Example: title ===

If html contains links in form of <a href="!http://some.domain.com/download?id=1245932" title="Podcast.2010-01-02.mp3">Download</a> the extracted title would be "Podcast.2010-01-02.mp3"

=== Example: link ===

If html contains links in form of <a href="!http://some.domain.com/download?id=1245932">Podcast.2010-01-02.mp3</a> the extracted title would be "Podcast.2010-01-02.mp3"

== Titles are gibberish ==

In some cases the titles are completely useless, however you may still get good filenames when entry is downloaded. This is because servers often send the correct filename in http headers. Of course when titles are useless filtering becomes much more troublesome.

== Get only certain links ==

In case page contains too many links, you can use regexps to select only certain links.

=== Example ===

{{{
html:
  url: <url>
  links_re:
    - domain\.com
}}}

This will create only entries from links which match any of given regexps. Do NOT use this for filtering content, just limit selecting to correct type of links and use real filtering plugins like [wiki:Plugins/regexp regexp] to do actual filtering.

== Basic Authentication ==

This plugin supports baisic authentication, it can be specified in the url:

{{{
html: http://username:password@url.com
}}}

Or as parameters:

{{{
html:
  url: <url>
  username: <username>
  password: <password>
}}}

== Dump ==

You can dump the received HTML into a file by using parameter {{{dump}}}. Useful for debugging.

=== Example ===

{{{
html:
  url: <url>
  dump: file.html
}}}
