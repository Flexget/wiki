---
title: ExecuteArguments
description: 
published: true
date: 2022-09-18T05:28:46.416Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:49:26.915Z
---

| Argument | Description |
| --- | --- |
| `--tasks <task> [<task> ...]` | Run only specified task(s), optionally using glob patterns ("tv-*"); matching is case-insensitive |
| `--learn` | Matches are not downloaded but will be skipped in the future |
| `--no-cache` | Disable caches; works only in plugins that have explicit support |
| `--stop-waiting <name>` | Stop [timeframe](/Plugins/series/timeframe) for a given series |
| `--disable-tracking` | Disable [episode advancement](/Plugins/series/tracking) for this run |
| `--tail-reset <file|task>` | reset [tail position](/Plugins/tail) for a file or an entire task
| `--discover-now` | Immediately try to discover everything, bypassing the `discover` option [`interval`](/Plugins/discover#interval) |
| `-T NAME, --template <name>` | Execute tasks using given template |
| `--now` | Run task(s) even if the [`interval` plugin](/Plugins/interval) would normally prevent it |
| `-v, --verbose` | Verbose undecided entries |
| `-s, --silent` | Don't verbose any actions (accept, reject, fail) |
| `--dump-config` | Display the config of each task after template merging/config generation occurs |
| `--dump [{eval,trace,accepted,rejected,undecided,title} [{eval,trace,accepted,rejected,undecided,title} ...]]` | Display all entries in task with fields they contain. Use `--dump eval` to evaluate all lazy fields; specify an entry state or states to only dump matching entries |
| `--dl-path <path>` | Override path for download plugin; this applies to all executed tasks |
| `--cli-config <variable=value> [<variable=value> ...]` | Use [dynamic configuration values](/Plugins/--cli-config) to replace keywords in your configuration file |
| `--try-regexp` | try regular expressions interactively |