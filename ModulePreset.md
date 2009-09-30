= Module Preset =

Works exactly like classic global section, but allows additionally multiple different presets.

{{{
global:
  download: ~/download/

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
    preset: movies

  # Note: This feed will use global because preset is built in (always enabled) and has default value of global
  fourth_feed:
    rss: http://example4.com
}}}