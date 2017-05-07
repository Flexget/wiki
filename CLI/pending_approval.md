---
import:
  - TableStylesDiv
---

## [CLI](/CLI) > `pending`
View and manage entries [`pending_approval`](/Plugins/pending_approval).

### Sub-commands
| Sub-command | Option | Description |
| --- | --- | --- |
| `list`* | List pending entries |
|| *optional:* ||
|| `--task-name <task_name>` | Filter by task name |
|| `--approved` | Show only approved entires|
|| `--pending` | Show only pending entires|
| `approve` || Approve pending entries |
|| *positional:* ||
|| `selection (entry_id|all)` | Approve one pending entry by ID, or all pending entries |
| `reject` || Reject pending entries |
|| *positional:* ||
|| `selection (entry_id|all)` | Reject one pending entry by ID, or all pending entries |
| `clear` | Clear all unapproved pending entries |
|| *optional:* ||
|| `--task-name <task_name>` | Filter by task name ||
|||{{> TableStylesDiv }}|

### Examples
```bash
# List all pending entries
flexget pending list

# Approve all pending entries
flexget pending approve all
```