---
title: Emit
description: 
published: true
date: 2022-09-18T04:57:50.425Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:57:47.892Z
---

# Emit cleanup
### Problem description
We currently have multiple plugins with various different naming and configuration convention. These should be unified.

**Group A**

* trakt_emit
* sonarr_emit
* uoccin_emit 

**Group B**

* emit_digest
* emit_series

**Group C**

* from_deluge
* from_rtorrent
* from_transmission

**Group D**

Badly named

* dynamic_imdb

this is basically emit from imdb with configuration

### Thoughts
* emit is a bit weird term and "from_deluge" etc seem to make more sense than "emit_deluge"
* emit_series and trakt_emit are a bit different as they are automatically generated sequences based on current status .. they should be called "next_series" and "next_trakt" ?
* rename everything to "from_<thing>" / "next_<thing>"
