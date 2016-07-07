# Free Space
This plugin will abort a task if free space on a given drive is getting low.


| **Option** | **Description** |
| --- | --- |
| path | The path that you want to monitor for space. |
| space | Amount of free space (in MB) that you require for new entries to be allowed. |

**Example**

```
free_space:
  path: /location/to/monitor
  space: 500
```