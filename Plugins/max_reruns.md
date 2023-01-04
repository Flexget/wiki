---
title: max_reruns
description: 
published: true
date: 2023-01-04T16:18:19.703Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:08:01.604Z
---

# Max Reruns

Simple plugin that limits the number of reruns a specific task is allowed to perform consecutively. Useful for limiting the number of reruns [discover](discover) performs.

### Example

```YAML
  download-task:
    series:
      - Some Awesome Show
    discover:
      what:
        - next_series_episodes: yes
      from:
        - some_search_plugin: yes
    max_reruns: 3
```