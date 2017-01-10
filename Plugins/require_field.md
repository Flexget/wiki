# Require field
This plugin will reject any [entries](/Entry) that do not have the specified [fields](/Entry#Knownfields). Also rejects if specified field is present, but is an empty string.

**Example:**

This example does the same thing as the [imdb_required](/Plugins/imdb_required) plugin. (As long as [imdb_lookup](/Plugins/imdb_lookup) is also enabled on the task.)
```
require_field: imdb_id
```

**Example:**

This example will reject entries that do not have parsed series information.
```
require_field:
  - series_name
  - series_season
  - series_episode
```