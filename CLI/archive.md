## `archive`
Search and manipulate the archive database

### Actions
| action | description |
| --- | --- |
| `search` | Search from the archive |
| `inject` | Inject entries from the archive back into tasks |
| `tag-source` | Tag all archived entries within a given source | 
| `consolidate` | Migrate old archive data to new model, may take a long time |

### Examples
```bash
#searches the archive for "foo"
flexget archive search "foo"
```

### Related articles
* [CUI / Command line interface overview](/CLI)
* [archive Plugin](/Plugins/archive)