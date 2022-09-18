---
title: search_rss
description: 
published: true
date: 2022-09-18T05:12:13.923Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:12:11.388Z
---

# Seach RSS

A generic search plugin that can use rss based search feeds. Configure it like rss
plugin, but include `{{search_term}}` in the url where the search term should go.

**Example:**

Combine with discover plugin to search movies from rss feed.

```yaml
discover:
  what: 
    - movie_list: movies
  from:
    - search_rss: "http://domain.org&q={{ search_term }}"
```