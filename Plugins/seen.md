# Seen
Remembers downloaded entries across all tasks and rejects them on subsequent executions.

This plugin is enabled on all tasks by default. See plugin [disable_builtins](/Plugins/disable_builtins) for information how to disable builtin plugins. Note that disabling this will (likely) cause FlexGet to download all matches on every execution!

## Local Mode
You may not want entries seen on some tasks to affect other tasks. Seen plugin can be put into local mode, such that it will only reject entries that have been accepted previously in the same task. You can use the following configuration to enable this mode:
```yaml
seen: local
```

## Using custom fields
By default, `seen` plugin will filter entries based on that following fields: `title`, `url` & `original_url`. You can choose to override this by using the plugin as such:
```yaml
seen:
  fields:
    - url
    - title
    - any other field name
```

You can use any field you want to filter, as long as at least one field is supplied. This feature was built in order to succesfully accept entries that have different urls but share the same `original_url`. Can be used as such:
```yaml
seen:
  local: yes
  fields: [title, url]
```
Using this will disregard the `original_url` attribute. 

## Commandline usage
The plugin has a few command line options. You may use the CLI help for syntax info (`flexget seen --help`) or visit the [`seen` CLI wiki entry](/CLI/seen) for more examples in usage.