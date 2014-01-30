== Goals ==

- Have a standardized framework for metainfo providers, so that plugins which require metainfo aren't coupled so tightly to one specific metainfo provider.
- Let the user customize priority and which providers are allowed in the task.
- Allow requesting a metainfo lookup for a certain category (series, movies, etc.)

== Configuration ==

Suggested formats:

{{{
metainfo:
  type: series
  provider: trakt
}}}
----------------
Alternate idea: metainfo providers are configured at the root of the config. This way, even things like cli utilities (movie queue) can request a lookup which can use the users settings.
{{{
tasks:
  a:
    metainfo: series
# Optional customization of metainfo providers:
metainfo_providers:
  series:
    - trakt
  movies:
    - imdb
    - tmdb
}}}

''TODO: MORE''