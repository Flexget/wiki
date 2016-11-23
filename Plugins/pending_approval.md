# Pending approval
A manual operation filter plugin. Stores entries in local cache until their status is set to approved via CLI or API. All approved entries will be accepted in filter phase.  
Used to cherrypick entries from a source.

Accepted pending entries (those that were approved) will be deleted from the cache.

### Schema:
```yaml
pending_approval: [yes/no]
```

### Usage example:

```yaml
tasks:
  pending_task:
    rss: http://bla.com
    pending_approval: yes
    download: /downloads/
    no_entries_ok: yes
```
In this example all the entries that the RSS feed outputs will be sent to the `pending_approval` plugin. Once approved, they will be accepted (the next time the task runs) and passed to `download` plugin.

*****Note:***** Since all intially added entries will be cached and removed, it may seem that task did not produce entries at the first run (and hence the [no_entries_ok](/Plugins/no_entries_ok) usage). The task will appear to have input only when it's proccessing approved entries.

### Approving entries:

There are currently two ways of approving entries: CLI and API.

####  CLI:
- View all pending entries: `flexget pending list`  
- Approve a pending entry: `flexget pending approve <ENTRY_ID>`  

View `pending_approval` [CLI page](/CLI/pending_approval) for more details and options.

#### API

View swagger documentation for endpoint details.

### Advanced usage example using entry list:
```yaml
tasks:
  filter_before_pending:
    rss: http://foo.com
    quality: 720p # An example for a filter
    list_add:
      - entry_list: pending_entries
    pushover: <OPTS> # Get notified about new items added to the entry list
    seen: local # This is a must or entries will be rejected on the download task
  
  approved:
    entry_list: pending_entries
    pending_approval: yes
    list_remove: # Use this to clear data from the entry list. Optional
      - entry_list: pending_entries
    download: /downloads/
      
```
This example shows how to filter before using the `pending_approval` plugin. Also, this is the way to get notification aobut new items added to `pending_approval` plugin.
  
  




