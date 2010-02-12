= Directories =

Parses any simple directory and use it as input.

=== Example ===

{{{
listdir: /storage/movies/
}}}

=== Multiple directories ===
{{{
listdir:
  - /storage/movies/
  - /storage/series/
  - ... and so on
}}}

=== Additional usage ===
Some times it's better to generate RSS directly from directories instead of the ordinary ones by using make_rss:
{{{
 listdir: - /storage/movies
 accept_all: yes
 make_rss:
   file: /storage/rss.rss
   days: 1
}}}