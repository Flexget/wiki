---
import:
  - ExecuteArguments
---


## [CLI](/CLI) > `execute`
Execute tasks now. If FlexGet is not running as a [daemon](/Daemon) or via [cron](/InstallWizard/Partial/Crontab), this is the only way tasks can be executed.

### Arguments
{{> ExecuteArguments }}

### Examples
```bash
#executes the "foo_task"
flexget execute --tasks foo_task
```