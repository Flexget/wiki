## `database`
Utilities to manage the FlexGet database

### Actions
| action | option | description |
| --- | --- | --- |
| `cleanup` || Make all plugins clean un-needed data from the database |
| `vacuum` || Running vacuum can increase performance and decrease database size |
| `reset` || Reset the entire database (DANGEROUS!) |
|| `--sure` | You will need to use this argument if you really want to reset the database. You don't do you? |
| `reset-plugin` || Reset the database for a specific plugin |
|| `<plugin name>` | Name of the plugin to reset |

### Examples
```bash
#cleanup database from un-needed data
flexget database cleanup
```

### Related articles
* [CUI / Command line interface overview](/CLI)