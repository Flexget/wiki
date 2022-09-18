---
title: tvt
description: 
published: true
date: 2022-09-18T05:15:43.559Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:15:40.980Z
---

# TVTorrents
**Plugin seems to be broken at the moment and there's nobody to maintain it**

A customized HTML input module. Parses out full torrent URLs from [TVTorrents](http://tvtorrents.com)' page for recently aired TV show episodes.

May break in the future, as it depends on the exact structure of the HTML.

Plugin-specific code by Fredrik Bränström.

## Usage
Just set **tvt: yes** and configure [cookies](/Plugins/cookies) plugin.

## Example
```
tasks:
  TVTorrents:
    tvt: yes
```
