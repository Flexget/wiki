---
title: passthepopcorn
description: 
published: true
date: 2022-12-07T05:46:59.651Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:18:20.861Z
---

# PassThePopcorn
> This plugin is part of [search](/Plugins/Searches) plugin system
{.is-success}

This search plugin will get movie results from PassThePopcorn.

## Configuration
`username`, `password` and `passkey` are required. Everything else is optional. Your passkey is visible on your PTP profile page or in any download link on the site. It uniquely identifies you, so keep it secret, keep it safe.

The option `grouping` affects how `order_by` and `order_desc` influences search results. With it on, it sorts results by release group, without it, it sorts by individual torrents uploaded.

NOTE: `freeleech: no` removes all freeleech results.
```
passthepopcorn:
  username: myusername (required)
  password: mypassword (required)
  passkey: mypasskey (required)
  tags:
    - list of tags
  order_by: see below
  order_desc: yes|no (default yes)
  freeleech: yes|no (default neither)
  release_type: non-scene|scene|golden popcorn
  grouping: yes|no (default yes)
```
### Tags
Choose one or more of the following tags:
- action
- adventure
- animation
- arthouse
- asian
- biography
- camp
- comedy
- crime
- cult
- documentary
- drama
- experimental
- exploitation
- family
- fantasy
- film.noir
- history
- horror
- martial.arts
- musical
- mystery
- performance
- philosophy
- politics
- romance
- sci.fi
- short
- silent
- sport
- thriller
- video.art
- war
- western

### Order by
- Relevance
- Time added
- Time w/o reseed
- First time added
- Year
- Title
- Size
- Snatched
- Seeders
- Leechers
- Runtime
- IMDb rating
- IMDb vote count
- PTP rating
- PTP vote count
- MC rating
- RT rating
- Bookmark count