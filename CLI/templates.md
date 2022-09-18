---
title: templates
description: 
published: true
date: 2022-09-18T05:01:20.956Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:54:40.785Z
---

## [CLI](/CLI) > `templates`*
View file templates to be used with [notifer](/Plugins/Notifiers) plugins.

### Optional arguments
|  Argument | Description |
| --- | --- |
|`--name <template_name>`| Filter by `<template_name>`
{{> Includes/TableStylesDiv }}

### Examples
```bash
# Shows all templates
$ flexget templates

# Filters by name 'rss'
$ flexget templates --name rss
```