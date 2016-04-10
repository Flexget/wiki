=== List Queue ===

This plugin is a [wiki:Plugins/List/ list_interface] plugin.

Using `list_queue` will accept any entry matching contents of list and immediately remove the matched element from the list:
{{{
discover:
  interval: 3 hour
    what:
      - movie_list: Looking
    from:
      - kat:
          verified: yes
      - torrentz: verified
list_queue:
  - movie_list: Looking
download: /downloads/
}}}

This plugin is useful when input list and filter list are matching, as in the example above. In order to keep a list of downloaded movies, another list can be create/added to on output:
{{{
discover:
  interval: 3 hour
    what:
      - movie_list: Looking
    from:
      - kat:
          verified: yes
      - torrentz: verified
list_queue:
  - movie_list: Looking
download: /downloads/
list_add:
  - entry_list: downloaded movies
}}}
