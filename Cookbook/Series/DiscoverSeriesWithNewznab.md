---
title: DiscoverSeriesWithNewznab
description: 
published: true
date: 2022-09-18T05:20:43.019Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:20:40.443Z
---

# Discover nzb files from Newznab
This recipe will cause FlexGet to search for series episode using a newznab website rather than using a RSS feed. This can be helpful if you want to download series episode for older Series that wouldn't normally appear in a newznab RSS, but are indexed by the newznab website.

First in your task you need to set which series you want to download, then we will use the discover episode to search on newznab our episodes (through the emit_series plugins).


To configure the newznab episodes you need to provide :
- The website
- Your apikey
- Category type to search on newznab
- Wait time between two calls on the website (this can lower load on the newznab server).

```
tvsearch:
  domain_delay:
    www.xxxxxx.com: 3 seconds
  series:
     720p+:
        - Your lovely show 1
        - Your lovely show 2
  discover:
     what:
       - emit_series: yes
     from:
       - newznab:
           website: "http://www.xxxxxx.com/"
           apikey: "xxxxxxxxxxxxxxxxxxxxxxxxxx"
           category: tv
  sabnzbd:

```