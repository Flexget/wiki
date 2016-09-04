## `database`
Utilities to manage the FlexGet database

### Actions
| action | description |
| --- | --- |
| `cleanup` | Make all plugins clean un-needed data from the database |
| `vacuum`| Running vacuum can increase performance and decrease database size |
| `reset` | Reset the entire database (DANGEROUS!) |
| `reset-plugin` | Reset the database for a specific plugin | 

### Examples
```bash
#cleanup database from un-needed data
flexget database cleanup
```

### Related articles
* [CUI / Command line interface overview](/CLI)