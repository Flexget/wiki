= RSS =

Parses RSS feed.

Simple configuration:

{{{
rss: <url>
}}}

Configuration with basic http authentication:

{{{
rss:
  url: <url>
  username: <name>
  password: <password>
}}}

Configuration with saved cookies:

{{{
rss:
  url: <url>
  cookie:
    type: mozilla
    file: /path/to/cookie
}}}

Possible cookie types are: mozilla, msie, lpw