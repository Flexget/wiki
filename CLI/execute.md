## `execute`<a name="execute"></a>
execute tasks now

### Optional arguments
| argument | description |
| --- | --- |
| `--tasks TASK [TASK ...]` | run only specified task(s), optionally using glob patterns ("tv-*"). matching is case-insensitive
| `--learn` | matches are not downloaded but will be skipped in the future 
| `--no-cache` | disable caches. works only in plugins that have explicit support |
| `--stop-waiting NAME` | stop timeframe for a given series |
| `--disable-tracking` | disable episode advancement for this run |
| `--tail-reset FILE|TASK` | reset tail position for a file |
| `--discover-now` | Immediately try to discover everything |
| `-T, --template NAME` | execute tasks using given template |
| `--now` | run task(s) even if the interval plugin would normally prevent it |
| `-v, --verbose` | verbose undecided entries |
| `-s, --silent` | don't verbose any actions (accept, reject, fail) |
| `--dump-config` | display the config of each feed after template merging/config generation occurs |
| `--dump [{eval,trace,accepted,rejected,undecided,title} [{eval,trace,accepted,rejected,undecided,title} ...]]` | display all entries in task with fields they contain, use `--dump eval` to evaluate all lazy fields. Specify an entry state/states to only dump matching entries. |
| `--dl-path PATH` | override path for download plugin, applies to all executed tasks |
| `--cli-config VARIABLE=VALUE [VARIABLE=VALUE ...]` | configuration parameters through commandline |
| `--try-regexp` | try regular expressions interactively |

### examples
```bash
#executes the "foo_task"
flexget execute --tasks foo_task
```
### Related articles
* [CUI / Command line interface overview](/CLI)
* Not to be confused with the [Exec plugin](/Plugins/exec)