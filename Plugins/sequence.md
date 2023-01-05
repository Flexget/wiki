---
title: sequence
description: 
published: true
date: 2023-01-05T02:28:25.121Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:12:34.200Z
---

# Sequence

Mainly for advanced usecases. Run any plugins in order. 

### Simple Example

```yaml
sequence:
  - rss: http://example1.com
  - rss: http://example2.com
```
Note: Using [inputs](/Plugins/inputs) plugin would be more appropriate use for this usecase.

### Advanced Example

Here we using the [configure_series](/Plugins/configure_series) plugin using two separate Trakt lists, and applying a different set of settings to each list. This could then be used with the [discover](/Plugins/discover) plugin in a task

```yaml
    sequence:
      - configure_series:
          from:
            <<: *trakt_tv_list
          settings:
            target: 1080p hdtv+
            quality: 1080p webrip+
            timeframe: 18 hours
      - configure_series:
          from:
            <<: *trakt_tv4k_list
          settings:
            quality: 2160p webrip+ !dolbyvision
```
