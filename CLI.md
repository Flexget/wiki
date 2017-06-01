# Command Line Interface (CLI)
FlexGet is usually invoked as a [Daemon](/Daemon) or via [cron](/InstallWizard/Partial/Crontab), configured with its [configuration](/Configuration) file. Many functions can also be performed on the command line. The following information can be seen on the command line by invoking `flexget --help` or the equivalent `flexget -h`.

There are several [root-level environment variables](/EnvironmentVariables) which can be set to determine the default behavior of FlexGet. Environment variables which apply to specific CLI commands are documented on that command's page.

## Usage
FlexGet is invoked from the command line like so:
```bash
flexget <argument> [<argument> ...] <command> <command-arguments>
```
For example, the FlexGet configuration file can be tested by calling `flexget check`. This does nothing to harm your installation so you can always run this (and it is recommended to be the first command used after [upgrading](/Upgrade)).

### `<command>`
In the above example, `check` is the `<command>` being used. 

### `<argument>`
One-letter "shortcut" arguments are prefixed with a single dash (`-`). The long form of arguments are prefixed with two dashes (`--`).

Some arguments are directed to FlexGet itself, such as `--loglevel`. They change the overall settings of the FlexGet operation or output. These are placed before the command when invoking FlexGet.

Most commands also have arguments. In the command `flexget execute --tasks task_name`, `--tasks task_name` is an argument to the `execute` command. These direct specific commands to operate in certain ways, or to perform particular functions, such as executing the task named `task_name` in the above example. Because they affect specific commands, they follow those commands when invoking FlexGet.

Some commands will have mandatory arguments called positional arguments or actions. These are not prefixed and look like commands. FlexGet has a lot of list-type options/arguments. These usually support different [output table styles](/CLI/--table-styles).

## Commands
Clicking on the commands will take you to a page with more information about it.
| Command | Description |
| --- | ---|
| [`archive`](/CLI/archive) | Search and manipulate the archive database|
| [`backlog`](/CLI/backlog) | View or clear entries from the [`backlog`](/Plugins/backlog) plugin |
| [`check`](/CLI/check) | Validate [configuration file](/Configuration) and print errors |
| [`daemon`](/CLI/daemon) | Run continuously, executing tasks according to [schedules](/Plugins/Daemon/scheduler) defined in config |
| [`database`](/CLI/database) | Utilities to manage the FlexGet database |
| [`doc`](/CLI/doc) | Display [plugin](/Plugins) documentation |
| [`entry-list`](/CLI/entry-list) | View and manage [entry lists](/Plugins/List/entry_list) |
| [`jinja-filters`](/CLI/Jinja-Filters)| View avaialble [Jinja](/Jinja) filters
| [`execute`](/CLI/execute) | Execute tasks now |
| [`failed`](/CLI/failed) | List or clear remembered [failures](/Plugins/retry-failed) |
| [`history`](/CLI/history) | View the history of entries that FlexGet has accepted |
| [`inject`](/CLI/inject) | Inject an entry from command line into tasks |
| [`irc`](/CLI/irc) | View and manage [IRC](/Plugins/Daemon/irc) connections |
| [`movie-list`](/CLI/movie-list) | View and manage [movie lists](/Plugins/List/movie_list) |
| [`plugins`](/CLI/plugins) | Print registered plugin summaries |
| [`regexp-list`](/CLI/regexp-list) | View and manage [regexp lists](/Plugins/List/regexp_list) |
| [`rejected`](/CLI/rejected) | List or clear [remembered rejections](/Plugins/remember_rejected) |
| [`seen`](/CLI/seen) | View or forget entries remembered by the [`seen` plugin](/Plugins/seen) |
| [`series`](/CLI/series) | View and manipulate the [`series` plugin](/Plugins/series) database | 
| [`status`](/CLI/status) | View task health status |
| [`t4ll`](/CLI/t411) | View and manipulate the Torrent411 plugin database
| [`trakt`](/CLI/trakt) | View and manage [Trakt authentication](/Trakt_Authentication) |
| [`web`](/CLI/web) | Manage [web server](/Web-UI) settings |

## Root-level arguments
| Argument | Description |
| --- | --- |
| `-h, --help` | Show help message and exit. Note that most commands support this as an argument to the command as well, such as `flexget series show -h` for help on how to use `series show`. This particular argument always follows the command (and any arguments to the command). |
| `-V, --version` | Print FlexGet version and exit. |
| `--test` | Copies the database and executes task(s) in a testing mode. Prints a `verbose` log of what would happen on normal execution. (Note some plugin network functionality is disabled during `--test`.)|
| `-c CONFIG` | Specify configuration file (optionally with path). Default: `config.yml` |
| `--logfile LOGFILE, -l LOGFILE` | Specify a custom logfile filename (optionally with path). Default: `flexget.log` in the config directory. |
| `--loglevel LEVEL, -L LEVEL` | Set the verbosity of the logger. Levels: `critical`, `error`, `warning`, `info`, `verbose`, `debug`, `trace` |
| `--bugreport` | Create a detailed bug report for use in reporting an issue on [GitHub](https://github.com/Flexget/Flexget/issues). Note that the output might contain _private_ data, such as URLs or IP addresses, so edit that out before posting or submitting it. |
| `--profile [OUTFILE]` | Use the Python profiler for this run to debug performance issues. |
| `--cron` | Used when executing FlexGet non-interactively. This allows background maintenance to run, disables stdout and stderr output, and reduces the logging level to `info`. |
| `--debug-warnings` | Elevate warnings to errors for debugging purposes, so a traceback is shown.
| `--debug-db-sessions` | Debug session starts and ends, for finding problems with database locks. |