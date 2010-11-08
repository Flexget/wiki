= RSS =

Parses any RSS feed.

== Simple configuration ==

{{{
rss: <url>
}}}

Note: https supported.

=== Basic http authentication ===

{{{
rss:
  url: <url>
  username: <name>
  password: <password>
}}}

=== Read from a file ===
You can also use local file instead of url.

''' Example '''

{{{
rss:
  url: /path/to/rss/something.xml
}}}

== Advanced usages ==

There are more advanced options that can be used with the rss plugin if you need them.

=== Link field ===
Incase RSS-feed uses some nonstandard field for {{{link}}} urls (ie. guid) you can
configure module to use url from any feedparser entry attribute.

'''Example'''

{{{
rss:
  url: <url>
  link: guid
}}}

=== Silent mode ===
You can disable few possibly annoying warnings by setting {{{silent}}} value to {{{yes}}} on feeds where there are
frequently invalid items.

'''Example'''

{{{
rss:
  url: <url>
  silent: yes
}}}

=== Group Links ===
If the feed has several links by item, you can set the {{{group links}}} value to {{{yes}}}. This way, only one entry will be generated for the item, with all links attached to it.
Links are enclosures plus item fields given by the {{{link}}} value, in that order.

The download plugin will then try to download each link until one works.

'''Example'''

{{{
rss:
  url: <url>
  group links: yes
}}}

=== Capture other fields ===
If you want to keep information in another rss field attached to the flexget [wiki:Entry entry], you can use the {{{other_fields}}} option.

'''Example'''
{{{
rss:
  url: <url>
  other_fields: [date]
}}}

=== Convert to ASCII ===

Some feeds contain unicode characters which may cause problems. To force these into ASCII you set the {{{ascii}}} option to {{{yes}}}.

{{{
rss:
  url: <url>
  ascii: yes
}}}

=== Private trackers ===

Some trackers are private and require that you use some form of authentication. One might want to try using the header plugin

{{{
header:
  cookie: 'uid=XXXXXXXXXXXXXXXX;pass=XXXXXXXXXXXXXXXXXXX'
rss:
  url: <url>
}}}
