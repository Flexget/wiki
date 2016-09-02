# CLI or FlexGet Command Line Interface
FlexGet is usually invoked as a [Daemon](/Daemon) or via [cron](/InstallWizard/Partial/Crontab) and its [configuration](/Configuration) file. The following information you can also get by invoking `flexget --help` or the equivalent `flexget -h`.

## Usage
You manually invoke FlexGet from the command line like so:
```bash
flexget <command> 
```
You could for example test your FlexGet configuration right now by calling `flexget check`. This does nothing to harm your installation so you can always run this. `check` is the `<command>` being used.

FlexGet can have arguments and commands can have arguments. Arguments are usually prefixed with `--`, sometimes with just one `-`.

## Arguments list
All FlexGet arguments are optional.
| argument | description |
| --- | --- |
| `-h, --help` | show this help message and exit |
| `-V, --version` | Print FlexGet version and exit. |
| `--test` | Verbose what would happen on normal execution. |
| `-c CONFIG` | Specify configuration file. Default: config.yml |
| `--logfile LOGFILE, -l LOGFILE` | Specify a custom logfile name/location. Default: flexget.log in the config directory. |
| `--loglevel LEVEL, -L LEVEL` | Set the verbosity of the logger. Levels: none, critical, error, warning, info, verbose, debug, trace |
| `--bugreport` | Use this option to create a detailed bug report, note that the output might contain PRIVATE data, so edit that out |
| `--profile [OUTFILE]` | Use the python profiler for this run to debug performance issues. |
| `--cron` | use when executing FlexGet non-interactively: allows background maintenance to run, disables stdout and stderr output, reduces logging level |
| `--debug-warnings` | elevate warnings to errors for debugging purposes, so a traceback is shown
| `--debug-db-sessions` | debug session starts and ends, for finding problems with db locks |

## Commands list
| command | description |
| --- | ---|
| [`execute`](#execute) | execute tasks now |
| [`daemon`](#daemon) | run continuously, executing tasks according to schedules defined in config |
| [`backlog`](#backlog) | View or clear entries from backlog plugin |
| [`seen`](#seen) | View or forget entries remembered by the seen plugin |
| [`doc`](#doc) | display plugin documentation |
| [`status`](#status) | View task health status |
| [`entry-list`](#entry-list) | view and manage entry lists |
| [`failed`](#failed) | list or clear remembered failures |
| [`plugins`](#plugins) | Print registered plugin summaries |
| [`web`](#web) | Manage web server settings |
| [`irc`](#irc) | View and manage irc connections |
| [`trakt`](#trakt) | View and manage trakt authentication |
| [`movie-list`](#movie-list) | View and manage movie lists |
| [`t4ll`](#t4ll) | view and manipulate the Torrent411 plugin database
| [`database`](#database) | Utilities to manage the FlexGet database |
| [`archive`](#archive) | Search and manipulate the archive database|
| [`check`](#check) | validate configuration file and print errors |
| [`history`](#history) | View the history of entries that FlexGet has accepted |
| [`rejected`](#rejected) | list or clear remembered rejections |
| [`inject`](#inject) | inject an entry from command line into tasks |

## Commands
This section gives detailed descriptions and examples of the available commands.

### `execute`<a name="execute"></a>
execute tasks now

#### arguments
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

#### examples
```bash
#executes the "foo_task"
flexget execute --tasks foo_task
```
#### Related articles
* Not to be confused with the [Exec plugin](/Plugins/exec)
### [`daemon`](/Daemon)<a name="daemon"></a>
run continuously, executing tasks according to schedules defined in config
#### actions
Unlike other commands daemon uses actions instead of arguments. No `--` here.
| action | description |
| --- | --- |
| start | start the daemon |
| stop | shutdown the running daemon |
| status | check if a daemon is running |
| reload | causes a running daemon to reload the config from disk |
#### examples
```bash
#starts the FlexGet daemon
flexget daemon start
#stops the FlexGet daemon
flexget daemon stop
```
#### Related articles
* [`daemon` Wiki article](/Daemon)
### `backlog`<a name="daemon"></a>
View or clear entries from backlog plugin
### [`seen`](/Plugins/seen)<a name="seen"></a>
View or forget entries remembered by the seen plugin
#### Related articles
* [`seen` Wiki article](/Plugins/seen)
### `doc`<a name="doc"></a>
display plugin documentation
### `status`<a name="status"></a>
View task health status
### `entry-list`<a name="entry-list"></a>
view and manage entry lists
### `failed`<a name="failed"></a>
list or clear remembered failures
### `plugins`<a name="plugins"></a>
Print registered plugin summaries
### `web`<a name="web"></a>
Manage web server settings
### `irc`<a name="irc"></a>
View and manage irc connections
### [`trakt`](/Plugins/trakt)<a name="trakt"></a>
View and manage trakt authentication
#### Related articles
* [`trakt` Wiki entry](/Plugins/trakt)
### [`movie-list`](/Plugins/List/movie_list)<a name="movie-list"></a>
View and manage movie lists
#### Related articles
* [`movie_list` Wiki entry](/Plugins/List/movie_list)
### `t4ll`<a name="t4ll"></a>
view and manipulate the Torrent411 plugin database
### `database`<a name="database"></a>
Utilities to manage the FlexGet database
### [`series`](/Plugins/series)<a name="series"></a>
Utilities to manage the FlexGet database
#### Related articles
* [`series` Wiki entry](/Plugins/series)
### [`archive`](/Plugins/archive)<a name="archive"></a>
Search and manipulate the archive database
#### Related articles
* [`archive` Wiki entry](/Plugins/archive)
### `check`<a name="check"></a>
validate configuration file and print errors
### `history`<a name="history"></a>
View the history of entries that FlexGet has accepted
### `rejected`<a name="rejected"></a>
list or clear remembered rejections
### `inject`<a name="inject"></a>
inject an entry from command line into tasks
