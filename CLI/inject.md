## `inject`
This command can inject an entry. It expects to be passed a title or a URL, or both. If only a URL is passed, Flexget attempts to find a suitable title from the response headers when that URL is requested. If even after this no title was found, the command will abort.

### Arguments
| argument | description |
| --- | --- |
| `title/url` | title or url of the entry to inject |
| `url` | url of the entry to inject |
| `--force` | prevent any plugins from rejecting this entry |
| `--accept` | accept this entry immediately upon injection
| `--fields NAME=VALUE [NAME=VALUE ...]` | |

### Execute arguments
If only a URL and no title is given, Flexget will attempt to find a title in the URL's response headers.
| argument | description |
| --- | --- |
| `--tasks TASK [TASK ...]` | run only specified task(s), optionally using glob patterns ("tv-*"). matching is case-insensitive |
| `--learn` | matches are not downloaded but will be skipped in the future |
| `--no-cache` | disable caches. works only in plugins that have explicit support |
| `--stop-waiting NAME` | stop timeframe for a given series |
| `--disable-tracking` | disable episode advancement for this run |
| `--tail-reset FILE|TASK` | reset tail position for a file `
| `--discover-now` | Immediately try to discover everything |
| `-T NAME, --template NAME` | execute tasks using given template |
| `--now` | run task(s) even if the interval plugin would normally prevent it |
| `-v, --verbose` | verbose undecided entries |
| `-s, --silent` | don't verbose any actions (accept, reject, fail) |
| `--dump-config` | display the config of each feed after template merging/config generation occurs |
| `--dump [{eval,trace,accepted,rejected,undecided,title} [{eval,trace,accepted,rejected,undecided,title} ...]]` | display all entries in task with fields they contain, use `--dump eval` to evaluate all lazy fields. Specify an entry state/states to only dump matching entries. |
| `--dl-path PATH` | override path for download plugin, applies to all executed tasks |
| `--cli-config VARIABLE=VALUE [VARIABLE=VALUE ...]` | configuration parameters through commandline |
| `--try-regexp` | try regular expressions interactively |

### Examples
```bash
#Example, passing both title and URL (for example if the remote server doesn’t return a filename in its response headers)
flexget inject "your.tv.show.s01e01.720p.web-dl.mkv" "http://example.com/torrents.php?id=33"
#Example, passing only a URL (will fail if no title can be determined)
flexget inject "http://example.com/torrents.php?id=33"
#Arguments for the execute command can be appended, for example to tell a particular task to run with the injected entry
flexget --test inject "http://example.com/your.tv.show.s01e01.torrent" --tasks yourtask --dump
```

### Related articles
* [CUI / Command line interface overview](/CLI)