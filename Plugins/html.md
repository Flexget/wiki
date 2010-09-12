= Html =

Parses urls from html page. Usefull on sites which have direct download links of any type (mp3, jpg, torrent, ...).

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

== Get only certain links ==

In case page contains too many links, you can use regexps to select only certain links.

=== Example ===

{{{
html:
  url: <url>
  links_re:
    - domain\.com
}}}

This will create only entries from links which match any of given regexps.

== Dump ==

You can dump the received HTML into a file by using parameter {{{dump}}}.

=== Example ===

{{{
html:
  url: <url>
  dump: file.html
}}}

== Title options ==

Some feeds contain links that have useless title (like 'DL', '1', '2'..). If you need better titles you can use option {{{title_from}}} to guess better title from url.

=== Example ===

{{{
html:
  url: <url>
  title_from: url
}}}

Other possible values are: `auto` ''(default)'', `url`, `title` and `link`. 

== Titles are gibberish ==

In some cases the titles are completely useless, however you may still get good filenames when entry is downloaded. This is because servers often send the correct filename in http headers ..

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