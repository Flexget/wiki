---
title: discover_refactor
description: 
published: true
date: 2022-09-18T04:58:40.345Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:58:37.728Z
---

Ideas for improvements to the discover plugin: (all names are open for improvements)

Add an `est_release` plugin, which would be used by the discover plugin to predict a release date for a given search entry. This would be an interface to media specific plugins, e.g. `series_release` or `movie_release`. Discover plugin would then check `est_release(entry)`, and if a date in the future was returned, it would not perform a search for that entry.

A more generic rate limiting system would be in place for any entries that did not get a result from `est_release`. This would be an option given to discover plugin as an interval, maybe `try_every`, or some better name. Unique entries in the `from` section of discover would have their last search time recorded, and would not be searched again until `try_every` has passed.

### Issues to Contemplate
- If emit_series has no innate knowledge from e.g. tvrage, it does not know when to switch seasons. This could possibly be solved by having it emit both the next episode of this season, plus the first episode of next season. But what happens if you are catching up on a show and both of those are available, then episode advancement may cause only the next season to start being accepted, even though there were more to be grabbed from the previous one.
- It would be nice if when catching up on a show, more than one episode could be searched for at a time. But how would emit_series know when to do this?