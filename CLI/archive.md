## `archive`
Search and manipulate the archive database

### Actions
| action | option | description |
| --- | --- | --- |
| `search`* | Search from the archive |
|| *positional:* ||
|| `<keyword>` | Keyword(s) to search for |
|| *optional:* ||
|| `--tags TAG [TAG ...]` | Tag(s) to search within |
|| `--sources SOURCE [SOURCE ...]` | Source(s) to search within |
| `inject` || Inject entries from the archive back into tasks |
|| *positional:* ||
|| `ID` | Archive ID of an item to inject |
|| *optional:* ||
|| `--immortal` | Injected entries will not be able to be rejected by any plugins |
|| *execute arguments:* ||
||| arguments for the `flexget execute` command are allowed here |
| `tag-source` || Tag all archived entries within a given source | 
|| *positional:* ||
|| `<source>` | The source whose entries you would like to tag |
|| `<tag>` |  The tag(s) you would like to apply to the entries |
| `consolidate` || Migrate old archive data to new model, may take a long time |
|<div align="right">\* supports [table-styles](/CLI/--table-styles)</div> ||

### Examples
```bash
#searches the archive for "foo"
flexget archive search "foo"
```

### Related articles
* [CLI / Command line interface overview](/CLI)
* [archive Plugin](/Plugins/archive)