## `pending`
View and manage [`pending_approval`](/Plugins/pending_approval) entries

### Actions
| action | option | description |
| --- | --- | --- |
| `list`* | List pending entries |
|| *optional:* ||
|| `--task-name TASK_NAME` | Filter by task name |
|| `--approved` | Show only approved entires|
|| `--pending` | Show only pending entires|
| `approve` || Approve pending entries |
|| *positional:* ||
|| `selection` | `ENTRY-ID` or `all` to approve all pending entries |
| `reject` || Reject pending entries |
|| *positional:* ||
|| `selection` | `ENTRY-ID` or `all` to reject all approved entries |
| `clear` | Clear all unapproved pending entries |
|| *optional:* ||
|| `--task-name TASK_NAME` | Filter by task name |
\* Supports [table-styles](/CLI/--table-styles)</div>

### Examples
```bash
# List all pending entries
flexget pending list
# Approve all pending entries
flexget pending approve all
```

### Related articles
* [CLI / Command line interface overview](/CLI)
* [`pending_approval` plugin](/Plugins/pending_approval) 