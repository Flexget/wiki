# CLI or FlexGet Command Line Interface
FlexGet is usually invoked as a [Daemon](/Daemon) or via [cron](/InstallWizard/Partial/Crontab) and its [configuration](/Configuration) file. The following information you can also get by invoking `flexget --help` or the equivalent `flexget -h`.

## Usage
You invoke FlexGet from the command line like so:
```bash
flexget <argument> <command>
```
You could for example test your FlexGet configuration right now by calling `flexget check`. This does nothing to harm your installation so you can always run this. `check` is the `<command>` being used. 

FlexGet can have arguments and commands can have arguments. Arguments are usually prefixed with `--`, sometimes with just one `-`. Some commands will have mandatory arguments called positional arguments or actions. These are not prefixed and look like commands.

## Commands list
Clicking on the commands will take you to the detail page of the command.
| Command | Description |
| --- | ---|
| [`execute`](/CLI/execute) | Execute tasks now |
| [`daemon`](/CLI/daemon) | Run continuously, executing tasks according to schedules defined in config |
| [`backlog`](/CLI/backlog) | View or clear entries from backlog plugin |
| [`seen`](/CLI/seen) | View or forget entries remembered by the seen plugin |
| [`doc`](/CLI/doc) | Display plugin documentation |
| [`status`](/CLI/status) | View task health status |
| [`entry-list`](/CLI/entry-list) | View and manage entry lists |
| [`failed`](/CLI/failed) | List or clear remembered failures |
| [`plugins`](/CLI/plugins) | Print registered plugin summaries |
| [`web`](/CLI/web) | Manage web server settings |
| [`irc`](/CLI/irc) | View and manage irc connections |
| [`trakt`](/CLI/trakt) | View and manage trakt authentication |
| [`movie-list`](/CLI/movie-list) | View and manage movie lists |
| [`t4ll`](/CLI/t4ll) | View and manipulate the Torrent411 plugin database
| [`database`](/CLI/database) | Utilities to manage the FlexGet database |
| [`series`](/CLI/series) | View and manipulate the series plugin database |
| [`archive`](/CLI/archive) | Search and manipulate the archive database|
| [`check`](/CLI/check) | Validate configuration file and print errors |
| [`history`](/CLI/history) | View the history of entries that FlexGet has accepted |
| [`rejected`](/CLI/rejected) | List or clear remembered rejections |
| [`inject`](/CLI/inject) | Inject an entry from command line into tasks |

## Options list
| Option | Description |
| --- | --- |
| `-h, --help` | Show help message and exit |
| `-V, --version` | Print FlexGet version and exit. |
| `--test` | Verbose what would happen on normal execution. |
| `-c CONFIG` | Specify configuration file. Default: config.yml |
| `--logfile LOGFILE, -l LOGFILE` | Specify a custom logfile name/location. Default: flexget.log in the config directory. |
| `--loglevel LEVEL, -L LEVEL` | Set the verbosity of the logger. Levels: `critical`, `error`, `warning`, `info`, `verbose`, `debug`, `trace` |
| `--bugreport` | Use this option to create a detailed bug report, note that the output might contain PRIVATE data, so edit that out |
| `--profile [OUTFILE]` | Use the python profiler for this run to debug performance issues. |
| `--cron` | Use when executing FlexGet non-interactively: allows background maintenance to run, disables stdout and stderr output, reduces logging level |
| `--debug-warnings` | Elevate warnings to errors for debugging purposes, so a traceback is shown
| `--debug-db-sessions` | Debug session starts and ends, for finding problems with db locks |