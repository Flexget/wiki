---
title: history
description: 
published: true
date: 2022-09-18T04:53:53.075Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:53:50.457Z
---

## [CLI](/CLI) > `history`*
View the history of entries that FlexGet has accepted.

### Optional arguments
| Argument | Description |
| --- | --- |
| `--limit <num>` | Limit to `<num>` results |
| `--search <term>` | Limit to results that contain `<term>` |
| `--task <task>` | Limit to results in specified `<task>` |
| `--short`, `-s` | Shorter output |
[Includes/TableStylesDiv](/Includes/TableStylesDiv){.include}

### Examples
```bash
#displays the accepted history in porcelain table format
$ flexget history --porcelain
```