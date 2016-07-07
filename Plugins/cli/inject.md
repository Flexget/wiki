# `inject` command
This command can inject an entry. It expects to be passed a title or a URL, or both. If only a URL is passed, Flexget attempts to find a suitable title from the response headers when that URL is requested. If even after this no title was found, the command will abort.

Example, passing both title and URL (for example if the remote server doesn't return a filename in its response headers): `flexget inject "your.tv.show.s01e01.720p.web-dl.mkv" "http://example.com/torrents.php?id=33"`

Example, passing only a URL: `flexget inject "http://example.com/torrents.php?id=33"` -- this will fail if no title can be determined.

Arguments for the `execute` command can be appended, for example to tell a particular task to run with the injected entry. Example: `flexget --test inject "http://example.com/your.tv.show.s01e01.torrent" --tasks yourtask --dump`.


| `--force` | Prevent any plugins from rejecting this entry |
| --- | --- |
| `--accept` | Accept this entry immediately upon injection |
| `--fields NAME=VALUE [NAME=VALUE ...]` | Fields to explicitly populate on the injected entry |

See `flexget inject --help` for full details, and see also [execute's --inject option](/Plugins/--inject).