## [CLI](/CLI) > `execute`
Execute tasks now. If FlexGet is not running as a [daemon](/Daemon) or via [cron](/InstallWizard/Partial/Crontab), this is the only way tasks can be executed.

### Optional arguments
| Argument | Description |
| --- | --- |
| `--tasks TASK [TASK ...]` | Run only specified task(s), optionally using glob patterns ("tv-*"); matching is case-insensitive
| `--learn` | Matches are not downloaded but will be skipped in the future 
| `--no-cache` | Disable caches; works only in plugins that have explicit support |
| `--stop-waiting NAME` | Stop timeframe for a given series |
| `--disable-tracking` | Disable episode advancement for this run |
| `--tail-reset FILE|TASK` | Reset tail position for a file |
| `--discover-now` | Immediately try to discover everything, bypassing the `discover` option [`interval`](/Plugins/discover#interval) |
| `-T, --template NAME` | Execute tasks using given template |
| `--now` | Run task(s) even if the [`interval` plugin](/Plugins/interval) would normally prevent it |
| `-v, --verbose` | Verbose undecided entries |
| `-s, --silent` | Don't verbose any actions (accept, reject, fail) |
| `--dump-config` | Display the config of each feed after template merging/config generation occurs |
| `--dump [{eval,trace,accepted,rejected,undecided,title} [{eval,trace,accepted,rejected,undecided,title} ...]]` | Display all entries in task with fields they contain. Use `--dump eval` to evaluate all lazy fields; specify an entry state or states to only dump matching entries |
| `--dl-path PATH` | Override path for download plugin; this applies to all executed tasks |
| `--cli-config VARIABLE=VALUE [VARIABLE=VALUE ...]` | Use [dynamic configuration values](/Plugins/--cli-config) to replace keywords in your configuration file |
| `--try-regexp` | Try regular expressions interactively |

### Examples
```bash
#executes the "foo_task"
flexget execute --tasks foo_task
```