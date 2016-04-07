= Entry List =

This plugin stores a copy of any entry that was added to it, and can be used in a variety of ways. 

This plugin is a [wiki:list_interface list_interface] plugin.

=== Schema ===
{{{
entry_list: <NAME>
}}}

=== Usage ===
As a [wiki:list_interface list_interface] plugin it follows the same list actions:
{{{
any_input: ...
filter: ...
list_add: 
  - entry_list: list name
}}}

It can be added as an additional output:
{{{
rss: ..
movie_queue: accept
list_add:
  - entry_list: downloaded movies
}}}
This will add all accepted entries to an `entry_list` with the name `list name`. It then later be used as an input itself. This can replace the [wiki:Plugins/digest digest] for example:

{{{
entry_list: downloaded movies
accept_all:
email: ...
}}}


Another example:
{{{
trakt_list: options
accept_all: yes
list_add:
  - entry_list: trakt shows
}}}

This can later be used with [wiki:Plugins/configure_series configure_series] which will avoid reaching trakt (with this example) every time you want to run the task:
{{{
configure_series:
  from:
    - entry_list: trakt shows
  ...
}}}

== Entry List API ==
`entry_list` plugin has full API support. See [http://discuss.flexget.com/t/flexget-rest-api/ API post] for details