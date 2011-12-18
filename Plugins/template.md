= Preset =

Allows multiple presets for feeds and a special global preset that is
applied to every feed.

{{{
presets:

  tv:
    series:
      - foo
      - bar
    download: ~/download/series/

  movies:
    imdb:
      min_score: 6.2
      min_votes: 5000
    download: ~/download/movies/

feeds:
  some_feed:
    rss: http://example.com
    preset: tv

  another_feed:
    rss: http://example2.com
    preset: movies

  third_feed:
    rss: http://example3.com
    preset: 
      - tv
      - movies

  # Note: This feed will use global because preset is built in (always
  # enabled) and has default value of global
  fourth_feed:
    rss: http://example4.com
}}}

The global preset can be disabled on a specific feed by including the special preset {{{no_global}}} i.e.
{{{
preset: no_global
}}}
or, if you also need to include other presets
{{{
preset:
  - no_global
  - preset_b
}}}

== Execute feeds with a given preset ==

To execute all feeds that have certain preset you can use `--preset NAME`

'''Examples:'''

{{{
--preset movies
}}}

{{{
--preset tv
}}}

== Merging limitations ==

In case you're using multiple presets in a feed and more than one preset has same plugin, they must be
configured in same format for merge to be possible.

'''Incompatible:'''

{{{
preset-a:
  series:
    - foo
    - bar

preset-b:
  series:
    settings:
      720p:
        timeframe: 12 hours
    720p:
      - xxx
      - yyy
}}}

Why is it incompatible?

''Preset-a'' has list under series where as ''preset-b'' has key value-pairs.

For merging to work they need to be in same format:

'''Compatible:'''

{{{
preset-a:
  series:
    normal:
      - foo
      - bar

preset-b:
  series:
    settings:
      720p:
        timeframe: 12 hours
    720p:
      - xxx
      - yyy
}}}

In which case the result is:

{{{
series:
  settings:
    720p:
      timeframe: 12 hours
  720p:
    - xxx
    - yyy
  normal:
    - foo
    - bar
}}}

Simple values cannot never be merged. So for example multiple `rss: <url>` or `include: <file>` cannot be defined within feed & preset. Include accepts list format for files so that can be used instead. 