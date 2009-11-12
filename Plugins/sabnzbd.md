= SABnzbd =

=== Example ===

{{{
sabnzbd:
  apikey: 123456
  url: http://localhost/sabnzbd/api?
  category: movies
}}}

'''Notes:'''

 * For some reason `localhost` and `127.0.0.1` doesn't seem to work (anymore). Use real NIC IP instead. ''(Example: 10.0.0.1)''

=== All possible parameters ===

{{{
sabnzbd:
  apikey: ...
  url: ...
  category: ...
  script: ...
  pp: ...
}}}

== Override category ==

By setting entry category you can specify category per item. To set this you can use for example plugins [wiki:Plugin/set set], [wiki:Plugin/manipulate manipulate].

See [wiki:Recipe/SeriesSabNZBd this recipe] for example how to set category from series name.