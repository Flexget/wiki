---
title: sceper
description: 
published: true
date: 2022-12-12T10:13:47.156Z
tags: abandoned
editor: markdown
dateCreated: 2022-09-18T05:12:03.764Z
---

# Sceper

> sceper.ws is returning 404, plugin should be removed
{.is-danger}

Uses sceper.ws category url as input.

**`NOTE:`** This plugin relies on urlrewriters to rewrite to a valid download link. Certain urlrewriters may need to be disabled on the task if they do not produce the download links, most notably `urlrewrite_redirect`.

#### Example:

```yaml
tasks:
  some-task:
    sceper: http://sceper.ws/category/tv-shows/tv-shows-x264
    disable_urlrewriters: [urlrewrite_redirect]
```