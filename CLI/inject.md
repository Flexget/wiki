---
title: inject
description: 
published: true
date: 2022-09-18T04:53:56.972Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:53:54.289Z
---

## [CLI](/CLI) > `inject`
Inject an entry from the command line.

### Description
`inject` expects to be passed a title, a URL, or both. If only a URL is passed, Flexget attempts to find a suitable title from the response headers when that URL is requested. If, even after this, no title was found, the command will abort.

Alternatively, you can use the [`execute` command](/CLI/execute) with the `--inject` argument.

### Arguments
| Argument | Description |
| --- | --- |
| `<title>` | Title of the entry to inject |
| `<url>` | Url of the entry to inject |
| `--force` | Prevent any plugins from rejecting this entry |
| `--accept` | Accept this entry immediately upon injection
| `--fields <entry_field=value> [<entry_field=value> ...]` | Populate additional fields in the entry |

### Arguments to execute task(s)
If only a URL and no title is given, Flexget will attempt to find a title in the URL's response headers.
[ExecuteArguments](/ExecuteArguments){.include}

### Examples
```bash
#Example, passing both title and URL (for example if the remote server doesn’t return a filename in its response headers)
$ flexget inject "your.tv.show.s01e01.720p.web-dl.mkv" "http://example.com/torrents.php?id=33"

#Example, passing only a URL (will fail if no title can be determined)
$ flexget inject "http://example.com/torrents.php?id=33"

#Arguments for the execute command can be appended, for example to tell a particular task to run with the injected entry
$ flexget --test inject "http://example.com/your.tv.show.s01e01.torrent" --tasks yourtask --dump
```