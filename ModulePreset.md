= Module Preset =

''To be included in 1.0''

Works exactly like classic global section, but allows multiple different presets.

{{{
global:
  download: ~/download/

tv:
  series:
    - foo
    - bar  

movies:
  imdb:
    min_score: 6.2
    min_votes: 5000

feeds:
  some_feed:
    rss: http://example.com
    preset: [global, tv]

  another_feed:
    rss: http://example2.com
    preset: [global, movies]

  third_feed:
    rss: http://example3.com
    preset: [global, movies]

  # Note: This will use global because preset is built in (always enabled) and has default value of global
  fourth_feed:
    rss: http://example4.com
}}}