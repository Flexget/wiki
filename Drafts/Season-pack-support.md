= Reasoning 

Season packs can be a great source quickly download/back filling required episodes.
With a well-formed season pack this would actually be preferable for back-filling. This would also empower the search plugin.

= Problem

* Flexget currently handles each torrent file as a unique entity, and season packs do not conform to that schema.
* Passing on parts of the torrent file is a feature not guaranteed to be supported in all torrent clients 
* At least one popular tracker has adopted removing all season episodes and reposting as season packs as soon as a season is complete.

= Proposed solution

* Series parser should know how to correctly match season packs.
* `season` will be added as a new DB entity. It will link to its relevant `episode` objects.
* Torrent files cannot but split so they will have to be downloaded as a whole. Even though some torrent client can set `skip_files` via its API, there is no generic way to do this, so we shouldn't even 

== Suggested modes:
Using season pack in a series should have several operational modes:

=== auto
The default mode. If used, decides whether a season pack should be download by parsing it, figuring out how many episodes it hold and then calculating how many episodes are already fetched in DB. If the number is below a certain default threshold, season pack will be fetched.
{{{
series:
  - My Series:
      season_packs: yes
}}}

A more fine tuned approach could be used like this:
{{{
series:
  - My Series:
      season_packs: 
        mode: auto
        threshold: 30  # Will fetch season pack if less than 30 percent of episodes were downloaded
}}}

=== always
Will fetch all matching season packs of the series.
{{{
series:
  - My Series:
      season_packs: always
}}}
=== manual
Will fetch all specific season packs only. Should take season numbers, range (?)

{{{
series:
  - My Series:
      season_packs: 1,2,5-6,9-
}}}
