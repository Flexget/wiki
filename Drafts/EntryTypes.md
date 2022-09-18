---
title: EntryTypes
description: 
published: true
date: 2022-09-18T04:57:54.227Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:57:51.618Z
---

# Adding a typing system to entries
Just some brainstorming, I'm thinking about adding a new system to entries, where it can declare what type of content it represents. Don't have all my ideas together yet, so this is super drafty.

Motivations:
- We deal a lot more with the concept of an entry representing a show, rather than a single episode, trakt_list, trakt_add etc. need to know what type of things an entry represent.
- Want a common framework, so that all plugins make sure to provide similar info about entries representing a similar thing.
- A plugin like trakt_lookup wants to check whether an entry represents a show/episode/movie easily before doing a lookup
- fields like imdb_id may refer to many different things, in the past many plugins assumed this meant the entry was a movie
- url is a mandatory field, but we have several types of tasks that deal with non-downloadable things now. We make up somewhat useless urls for that stuff now, that should never be downloaded. (but things like urlrewrite still try to run, even when the url is an imdb or trakt one, or a made up local one from mock plugin)

### Idea 1: field promises
Have a system where entries can be tagged with one or more types. Plugins often only want to operate on a certain type of entry. Being tagged with a type would imply that it has one or more fields available, for example:

|  Type  |  implied fields  |
| --- | --- |
| download | url |
| show | series_name |
| episode | series_name, series_id |
| movie | movie_name |
| torrent | url, torrent |
| file | location |
Issues:
- We'd probably want things like movie_year, but we might want to tag something as a movie even though we don't know the year, so we can't really promise that, but it would be nice to somehow have a more enforceable standard for plugins wanting to read/set that
- episodes can have multiple different numbering schemes, I put series_id as a required field, but what about things like series_season, and series_episode, which wouldn't exist for a dated episode
- Would something like an episode be tagged with both show and episode? Have some sort of hierarchy? For example lookup plugins currently provide 2 levels of info about an episode, that for the whole show, and that specific to an episode.