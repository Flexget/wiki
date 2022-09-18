---
title: bluray_lookup
description: 
published: true
date: 2022-09-18T05:02:40.048Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:02:37.361Z
---

# Blu-ray.com lookup

This plugin returns bluray information about movies and tv seasons from blu-ray.com. It cannot be used to lookup information about individual tv episodes, **only** tv seasons with (future) bluray releases.

This lookup plugin is not very reliable, it's mainly used for the bluray movie estimator used by [discover](discover).

#### Syntax

```yaml
bluray_lookup: yes
```
**Movie Metainfo**

| bluray_lookup Field  |  Description  |
| --- | --- |
| bluray_name |  Name on blu-ray.com  |
| bluray_year |  Release year  |
| bluray_disc_rating |  User submitted ratings on video/audio/disc quality  |
| bluray_rating |  Average score sourced from blu-ray.com user reviews  |
| bluray_studio |  Studio behind the show/movie  |
| bluray_genres |  Genres  |
| bluray_released |  BluRay release date (if any)  |
| bluray_certification | Certification eg. PG-13 |
| bluray_runtime |  Total season/movie runtime  |
| bluray_url |  Url on blu-ray.com  |
| movie_name |  Same as `bluray_name`  |
| movie_year |  Same as `bluray_year` |
