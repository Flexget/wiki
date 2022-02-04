# Series Remove
Removes accepted entries for series, season or episode from the [series](/Plugins/series) plugin database.

Similar to the CLI command [`flexget series remove`](/CLI/series)
```
series_remove: yes
```

## Options
The optional `forget` parameter will remove the entries from the *entire database* (including [seen](/Plugins/seen) plugin).

Similar to the CLI command [`flexget series forget`](/CLI/series)
```
series_remove:
  forget: yes
```