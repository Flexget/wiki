= RSS =

Parses any RSS feed.

== Simple configuration ==

{{{
rss: <url>
}}}

Note: https supported.

== Basic http authentication ==

{{{
rss:
  url: <url>
  username: <name>
  password: <password>
}}}

== Advanced usages ==

Incase RSS-feed uses some nonstandard field for urls (ie. guid) you can
configure module to use url from any feedparser entry attribute.

=== Example ===

{{{
rss:
  url: <url>
  link: guid
}}}

You can disable few possibly annoying warnings by setting silent value to True on feeds where there are
frequently invalid items.

=== Example ===

{{{
rss:
  url: <url>
  silent: True
}}}

If the feed has several links by item, you can set the "group links" value to True. This way, only one entry will be generated for the item, with all links attached to it.
Links are enclosures plus item fields given by the "link" value, in that order.

The download plugin will then try to download each link until one works.

=== Example ===

{{{
rss:
  url: <url>
  group links: True
}}}

== Convert to ASCII ==

Some feeds contain unicode characters which may cause problems. To force these into ASCII you set:

{{{
rss:
  url: <ul>
  ascii: yes
}}}

== Read from a file ==

You can also use local file instead of url.

=== Example ===

{{{
rss:
  url: /path/to/rss/something.xml
}}}
