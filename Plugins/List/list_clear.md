## List Clear
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; This is part of [managed list](/Plugins/List) plugin system.
</div>

This is a list plugin that clears the contents of the given lists.

### Syntax
```yaml
list_clear:
  what:
    - <list_type>: <list_name>
  phase: <task_phase>
```

Supported phases are `start, input, metainfo, filter, download, modify, output, learn, exit`.

By default, it will run in `start` phase.

### Use case examples:
This example shows you how to sync a list from Trakt in Flexget into an entry list, clearing it before filling.

```yaml
fill_series_list
  list_clear:
    what:
      - entry_list: trakt
  trakt_list:
      account: '{{secrets.trakt.account}}'
      list: '{{secrets.trakt.series}}'
      type: shows
  list_add:
    - entry_list: trakt
  accept_all: yes
```