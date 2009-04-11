= Settings block problems =

Currently only way to change series default settings is trough "settings block" which was a quick hack. It has few problems.

 * Affects all feeds
 * Cannot be validated without big changes
 * Difficult to implement in web-ui in the future

== Possible fixes ==

=== Solution 1 ===

Include settings in series module.

{{{
rss: http://example.com
series:
  settings:
    hd:
      quality: 720p
    anime:
      path: ~/torrents/anime/

  hd:
    - some series
    - another series
  sd:
    - third series
    - fourth series
  anime:
    - zoom zoom
    - pew pew
}}}

Cons:

 * A lot of containers (complex)

Pros:
 
 * No need to define a lot of per-series settings

=== More possible solutions? ===


== Feedback ==

Feel free to add: