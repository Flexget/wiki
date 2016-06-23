= Entry List =

This plugin is a [wiki:Plugins/List/ list_interface] plugin.

Stores a copy of any entry that was added to it, and can be used in a variety of ways. 

=== Schema ===

{{{
entry_list: <NAME>
}}}

=== Usage ===

As a [wiki:Plugins/List/ list_interface] plugin it follows the same list actions:

{{{
any_input: ...
filter: ...
list_add: 
  - entry_list: list name
}}}

It can be added as an additional output:

{{{
rss: ..
list_match:
  from:
    - movie_list: main movies
list_add:
  - entry_list: downloaded movies
}}}

This will add all accepted entries to an `entry_list` with the name `list name`. It then later be used as an input itself. This can replace the [wiki:Plugins/digest digest] for example:

{{{
entry_list: downloaded movies
accept_all: yes
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

== Entry list CLI ==

For detailed instruction about these CLI commands:
{{{
$ flexget entry-list -h
}}}


Entry list support CLI operations:

=== Return all entry lists names ===

{{{
$ flexget entry-list all
}}}

=== List entry from entrylists ===

{{{
$ flexget entry-list list <LIST_NAME>
}}}
Default <LIST_NAME> is `entries`. This is true for all CLI actions.
=== Show details about a specific entry ===

{{{
$ flexget entry-list show <LIST_NAME> <ENTRY>
}}}

`<ENTRY>` can be the ID displayed in `entry-list list` or exact entry title.

=== Add or Update a entry to or from an entry list ===

Using a title and original URL is require. You can also add additional identifiers in the following format:

{{{
$ flexget entry-list add <LIST_NAME> <ENTRY_TITLE> <ORIGINAL_URL> --attributes imdb_id=tt1234556 tmdb_id=1234
}}}

If the given entry list does not exist it will be created.

If the entry with the title exists on that list, its list of attributes will be replaced by given list of attributes (or removed if such a list was not given).

=== Removing an entry from entry list ===

{{{
$ flexget entry-list del <LIST_NAME> <ENTRY>
}}}
`<ENTRY>` can be the ID displayed in `entry-list list` or exact entry title.

=== Clearing an entire entry list ===

{{{
$ flexget entry-list purge <LIST_NAME>
}}}
== Entry List API ==

`entry_list` plugin has full API support. See [http://discuss.flexget.com/t/flexget-rest-api/ API post] for details