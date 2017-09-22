# Pending List
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; This is part of [managed list](/Plugins/List) plugin system.
</div>

Stores a copy of any entry that was added to it, and can be used in a variety of ways. Will only emit the entry after it has been approved via CLI/API. Very useful in creating a broad scoped task where you can cherry pick entries.  
See [managed_list](/Plugins/List/) how to use lists in general. 

### Configuration

```text
pending_list: <NAME>
```

## Examples


### Series premieres suggestions

```yaml
task:
  pending_new_shows:
    priority: 1
    rss: http://rss.site.com
    regexp:
      accept:
      - s01e01
    list_add:
    - pending_list: new_shows
    metainfo_series: yes
    trakt_lookup: yes
    notify:
      entries:
        title: 'New show detected'
        message: |+
          {{ trakt_series_name }} - {{ trakt_series_year }}
          {{ title }} 
        via:
        - pushover:
            user_key: KEY
    
  download_new_shows:
    priority: 2
    pending_list: new_shows
    accept_all: yes
    notify:
      task:
        via:
          email: ...
```

First task `pending_new_shows` will add all accepted entries to an `pending_list` with the name `new_shows`. It then later be used as an input itself in a `download_new_shows` task. **Only** entries that have been marked as approved in that specific list will appear as input in the `download_new_shows` task.


## Command line interface

Please see [commandline documentation](/CLI/pending-list)

## Entry List API
`pending_list` plugin has full JSON API support. See [API page](https://flexget.com/API) for details.