---
title: plugins
description: 
published: true
date: 2022-09-18T04:54:16.309Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:54:13.633Z
---

## [CLI](/CLI) > `plugins`
Print summaries for registered [plugins](/Plugins).

### Optional arguments
| Argument | Description |
| --- | --- |
| `--group <group>`* | Show plugins belonging to specify `<group>` |
| `--phase <phase>`* | Show plugins that act on specified `<phase>` |
| `--builtins`* | Show only [builtin](/Builtin) plugins |
[Includes/TableStylesDiv](/Includes/TableStylesDiv){.include}

### Examples
```bash
#shows all builtin plugins
$ flexget plugins --builtins
```