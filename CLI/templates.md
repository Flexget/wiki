## [CLI](/CLI) > `templates`
View file templates to be used with [notifer](/Plugins/Notifiers) plugins.

### Optional arguments
|  Argument | Description |
| --- | --- |
|`--name <template_name>`| Filter by `<template_name>`
||<div align="right">all support [table-styles](/CLI/--table-styles)</div>|

### Examples
```bash
# Shows all templates
flexget templates

# Filters by name 'rss'
flexget templates --name rss
```