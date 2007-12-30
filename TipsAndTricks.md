= Tips And Tricks =

Here you can find some clever YML tricks to make configuration easier. Check [wiki:GlobalSection global section] for some tips as well.

== Defining locations as variables ==

In case you have multiple download locations, or path is long, you may wish to use variables instead of typing full path on each download location.

Example:

{{{
locations:
  &series: ~/torrents/series
  &movies: ~/torrents/movies

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