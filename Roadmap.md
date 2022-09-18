---
title: Roadmap
description: 
published: true
date: 2022-09-18T04:51:37.974Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:51:35.314Z
---

# Roadmap
High level goals and ideas that should help focus the development and act as a basis for discussion.

## Web-UI
The primary goal the webui should be to allow using FlexGet for most common use-cases without needing to understand the configuration syntax at all. 

**Series**

* Manage series either internally or via external integration
* Configure RSS feeds to follow
* Enable automatic discovery

**Movies**

Features:

* Movie list (done already)
* Configure RSS feeds to follow
* Queue movies from external sources
* Enable automatic discovery

Most of these can be implemented easily by generating configuration for user in the backend. For example enabling automatic movie discovery should make a following configuration.

```
tasks:
  webui-movie-discover:
    discover:
      what:
        - movie_list: movies # user selection
      from:
        - # user selection
    template: [webui-movie-download](/webui-movie-download)
```

The UI should probably not be responsible for generating this configuration, rather some JSON API backend plugin which can then also update it if configuration changes. This will require some new backend plugin capabilities as plugins are currently unable to run if configuration is not valid.

The REST API for this would be quite simple, take in movie list(s) and source(s).

```
PUT /webui-movies/ {'movie-lists': [movies](/movies), 'from': [kickass](/kickass)}
```
GET request would just return same stuff.

The download client configuration would be implemented in another view which would generate the webui-movie-download template.

### Full configuration editor
While nice this is also very laborious to implement properly. Even when done rewards are not so immediate, people who know how to deal with the configuration get little benefits and others will likely find the configuration process to be tedious and hard to understand.