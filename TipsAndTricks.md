= Tips And Tricks =

Here you can find some advanced YML configuration tricks. Check [wiki:GlobalSection global section] for some tips as well.

== Defining download paths as variables (yaml-references) ==

In case you have multiple download locations, or path is long, you may wish to use variables instead of typing full path on each download location.

Example:

{{{
series: &series ~/torrents/series
movies: &movies ~/torrents/movies

feeds:
  feed A:
    download: *movies
  feed B:
    download: *movies
  feed C:
    download: *series
  feed D:
    download: *movies
    patterns:
      - pattern A
      - pattern B: *series
      - pattern C
}}}

Variables can also be defined on their first occurrence and then reused as needed.

{{{
---
feeds:
  feed A:
    download:  &movies ~/torrents/movies
  feed B:
    download: *movies
  feed C:
    download: &series ~/torrents/series
  feed D:
    download: *movies
    patterns:
      - pattern A
      - pattern B: *series
      - pattern C
...
}}}

== Extending feed configuration ==

In case you have similar feed configurations you can use use one of them as template, or create separate non-used template outside feeds list.

Example:

{{{
feeds:
  feed A: &template
    patterns:
      - pattern A
      - pattern B
    download: ~/path

  feed B:
    <<: *template
    ignore:
      - pattern C
}}}

In above example {{{feed B}}} also has everything configured in {{{feed A}}}. Later value is used in case of duplicate keywords.

== Making single must have list ==

You can use global section and [wiki:FilterUnconditionally] to make a neat must-have list.

{{{
global:
  unconditionally:
    - must have this
    - and that
    - and even this
feeds:
  .
  .
  .
}}}

Now these matches are downloaded unconditionally regardless of the feed they occur in.