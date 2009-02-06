= Module Preset =

''To be included in 1.0''

Works exactly like classic global section, but allows multiple different presets.

{{{
global:
  download: ~/download/

my_series:
  series:
    - foo
    - bar  

feeds:
  some_feed:
    rss: http://example.com
    preset: [global, my_series]
}}}

Built-in, uses global by default (ie. without any configuration).