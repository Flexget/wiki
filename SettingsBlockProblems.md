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
  defaults:
    enough: 720p
  names:
    - some series
    - another series
}}}

Cons:

 * Series must be listed in wrapper (names)
 * Wrapper is required even without defaults

=== Solution 2 ===

Write a separate module that changes settings for series.

{{{
rss: http://example.com
series_defaults:
  enough: 720p
series:
  - some series
  - another series
}}}

Cons:

 * May be problematic for web-ui if changes are stored in config

=== More possible solutions? ===


== Feedback ==

Feel free to add: