---
title: seen
description: 
published: true
date: 2023-08-17T02:02:09.882Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:54:25.155Z
---

## [CLI](/CLI) > `seen`
View or forget entries remembered by the [`seen` plugin](/Plugins/seen).

### Notes
The [`execute` option](/CLI/execute) `--learn` (optionally combined with `--tasks`) can be used to mark all entries that would be accepted as seen.

### Sub-commands
| Sub-command | option | description |
| --- | --- | --- |
| `forget` || Forget entry or entire task from seen plugin database |
|| `<value>` |  Title or URL of entry to forget |
| `add` || Add a title or URL to the seen database |
|| `<value>` | Title or URL to add |
| `search`* || Search text from the seen database |
|| `<search term>` | Term to search for |
[Includes/TableStylesDiv](/Includes/TableStylesDiv){.include}

All sub-commands support the `--task` option, which can be specified to only act on certain tasks. It can contain wildcards, or be specified more than once to select multiple tasks.

### Examples
```bash
#Adds the title "The Foo Movie" to the seen database
$ flexget seen add "The Foo Movie"

#Can be used to forget everything seen from the FooTask.
$ flexget seen forget --task FooTask *

#Can be used to remove any url, title or even imdb url which already has been seen once to be downloaded again
$ flexget seen forget <value>

#Can can be used to add any url, title or even imdb url as already seen  preventing them to be downloaded
$ flexget seen add <value>

#Especially useful when you have downloaded something manually outside FlexGet
seen add "http://example.com/torrents/1235321"
#With tasks using plugin seen_movies you can also use imdb id to mark any movie as already seen
$ flexget seen add tt0119698
```