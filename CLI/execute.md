---
import:
  - ExecuteArguments
---


## [CLI](/CLI) > `execute`
Execute tasks now. If FlexGet is not running as a [daemon](/Daemon) or via [cron](/InstallWizard/Partial/Crontab), this is the only way tasks can be executed.

### Arguments
If only a URL and no title is given, Flexget will attempt to find a title in the URL's response headers.

{{> ExecuteArguments }}

### Examples
```bash
#executes the "foo_task"
flexget execute --tasks foo_task
```