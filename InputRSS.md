= RSS =

Parses RSS feed.

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

== Convert to ASCII ==

Some feeds contain unicode characters which may cause problems. To force these into ASCII you set:

{{{
rss:
  url: <ul>
  ascii: true
}}}

== Read from a file ==

You can also use local file instead of url.

=== Example ===

{{{
rss:
  url: /path/to/rss/something.xml
}}}