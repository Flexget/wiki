---
title: set_series_begin
description: 
published: true
date: 2022-09-18T05:12:56.105Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:12:53.611Z
---

# Set series begin
This plugin sets the episode to start getting a series from, for each accepted entry with fields `series_name` (show title) and `series_id` (episode id, eg. S01E03).

### Example

Set series begin values from trakt:

```yaml
next_trakt_episodes:
  username: your_username
  password: your_password
  context: collected
  list: collection
accept_all: yes
set_series_begin: yes
```