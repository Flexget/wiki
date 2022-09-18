---
title: Jinja-Filters
description: 
published: true
date: 2022-09-18T04:53:14.971Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:53:12.250Z
---

## [CLI](/CLI) > `jinja-filters`
View available [Jinja](/Jinja) filters and their descriptions.

### Optional arguments
| Argument | Description |
| --- | --- |
| `--name <name>` | Filter by jinja filter name |


### Examples
```bash
# Displays all filters
$ flexget jinja-filters

# Filter by jinja filter name
$ flexget jinja-filters --name re_replace
```