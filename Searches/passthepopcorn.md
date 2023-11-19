---
title: passthepopcorn
description: 
published: true
date: 2023-11-19T04:07:19.722Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:18:20.861Z
---

# PassThePopcorn
> This plugin is part of [search](/Plugins/Searches) plugin system
{.is-success}

This search plugin will get movie results from PassThePopcorn.

## Configuration
`apiuser`, `apikey` and `passkey` are required. Everything else is optional. `apiuser` and `apikey` can be found in your profile under Edit > Security, you will need to regenerate them and save your profile if they are blank. Your `passkey` is visible on your PTP profile page or in any download link on the site. It uniquely identifies you, so keep it secret, keep it safe.

The option `grouping` affects how `order_by` and `order_desc` influences search results. With it on, it sorts results by release group, without it, it sorts by individual torrents uploaded.

> WARNING: The plugin sets a resonable rate limit for requests to the site, if you have domain_delay: defined in your task be careful you don't set a shorter rate or you could get auto banned from the site. ALWAYS check the wiki and forum on the site for the current rules on API / script access. 
{.is-warning}


NOTE: `freeleech: no` removes all freeleech results.
```
passthepopcorn:
  apiuser: myusername (required)
  apikey: myapikey (required)
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