= RSS =

Parses RSS feed.

== Simple configuration ==

{{{
rss: <url>
}}}

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
  url: <ul>
  link: guid
}}}