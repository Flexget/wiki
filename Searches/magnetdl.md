---
title: magnetdl
description: 
published: true
date: 2022-12-07T05:22:44.477Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:07:38.943Z
---

# Magnetdl

> This plugin is part of [search](/Plugins/Searches) plugin system
{.is-success}

Works as input or as a search plugin.

## Configuration

| Option | Default | Description |
| --- | --- | --- |
| category | - | One of 'software', 'movies', 'games', 'e-books', 'tv', 'music' |
| pages | 5 | How many pages to retrieve

There's intelligent caching to avoid retrieving pages which have already been processed.

## Examples

```yaml
magnetdl:
  category: tv
```