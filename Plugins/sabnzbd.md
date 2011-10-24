= SABnzbd =

=== Example ===

{{{
sabnzbd:
  key: 123456
  url: http://localhost/sabnzbd/api?
  category: movies
}}}

=== All possible parameters ===

{{{
sabnzbd:
  key: ...
  url: ...
  category: ...
  script: ...
  pp: ...
  username: ...
  password: ...
}}}

== Override category ==

By setting [wiki:Entry entry] category you can override / specify sabnzbd category per item. To set it you can use plugins like [wiki:Plugins/set set], [wiki:Plugins/manipulate manipulate].

See [wiki:Cookbook/Series/SeriesSabNZBd this recipe] for example how to set category from a series name.