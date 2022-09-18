---
title: inputs
description: 
published: true
date: 2022-09-18T05:07:03.227Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:07:00.655Z
---

# Inputs
This plugin allows you to configure the same [input plugin](/Plugins#Inputs) multiple times in one task.

**Notes:**
- If entries with duplicate titles or urls are found, only the first one seen will be added to the task.
- If there is an error while retrieving one of the inputs, the others will still be run.

**Example:**
```yaml
inputs:
  - find:
      path: /home/me/incoming
      mask: '*.torrent'
  - rss: http://feeda.com
  - rss: http://feedb.com
```