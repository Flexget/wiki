= How to file a bug report =

Include as much information as possible, preferably the feed configuration and relevant log messages. Remove all your personal information by replace them with *****.

When you include configuration or log lines into ticket, please use `{{{...}}}` wiki-formatting. This is because otherwise all the details appear in single line. Use preview button to see that information is readable.

'''Example, how it should be:'''

{{{
my config:
  rss: http://foobar.com
  series:
    - foo
    - bar
  download: ~/downloads
}}}

'''Without `{{{...}}}` this would look like:'''

my config:
  rss: http://foobar.com
  series:
    - foo
    - bar
  download: ~/downloads

Which is a bit hard to read ..

== Additional details (optional) ==

To get more information about process you can execute the problematic task with --debug flag, this information may be necessary sometimes to resolve the issue.

Example:

{{{
flexget exec --task NAME --debug
}}}
