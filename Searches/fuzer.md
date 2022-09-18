---
title: fuzer
description: 
published: true
date: 2022-09-18T05:17:52.098Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:17:49.520Z
---

# Fuzer
This search plugin will get results from Fuzer

## Configuration
Configuration requires rss_key, user_id, and cookie password.  
RSS key will be found in your Fuzer account preferences while username and password are your usual Fuzer login credentials. 
Cookie password correlates to the `fzr2password` of the session cookie, user id to `fzr2userid`. Use your browser's developer console to fetch this data while being logged in to Fuzer
```yaml
fuzer: 
  rss_key: [string]
  user_id: [int]
  cookie_password: [str]
  category: HD Movies
```
`Category` option can be on or more of the following: `HD Movies`, `XviD`,`Israeli HD Movies` `BRRip`, `Israeli Movies`, `DVDR`, `Dubbed Movies`, `HD Shows`, `Shows`, `Israeli HD Shows`, `Israeli Shows`, `Dubbed Shows`, `Anime`, `Movie Packs`, `Shows Packs`.<BR>
It can also be any integer of any category that is or isn't list here.
 
Example:
```yaml
fuzer: 
  rss_key: xxxxxxxxxxxxxxxxxxxx
  user_id: xxxxxx
  cookie_password: xxxxxx
  category:
    - HD Movies
    - 5 
    - Dubbed Movies
```