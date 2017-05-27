---
import:
  - Includes/TableStylesDiv
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