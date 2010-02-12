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
Some times it's better to generate RSS directly from directories instead of the ordinary ones by using [wiki:Plugins/make_rss make_rss]:
{{{
 listdir: /storage/movies
 accept_all: yes
 make_rss:
   file: /storage/rss.rss
   days: 1
}}}
This will make rss with every input accepted and make them last one day in the feed.

If you always want to generate complete list you should use [wiki:Plugins/disable_builtins disable_builtins].