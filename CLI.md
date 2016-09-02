# CLI or FlexGet Command Line Interface
FlexGet is usually invoked as a [Daemon](/Daemon) or via [cron](/InstallWizard/Partial/Crontab) and its [configuration](/Configuration) file. The following information you can also get by invoking `flexget --help` or the equivalent `flexget -h`.

## Commands
### execute
execute tasks now
### [daemon](/Daemon)
run continuously, executing tasks according to schedules defined in config

### backlog
View or clear entries from backlog plugin

### [seen](/Plugins/seen)
View or forget entries remembered by the seen plugin

```bash
TODO:
----------------------------------------------------------
doc                 display plugin documentation
status              View task health status
entry-list          view and manage entry lists
failed              list or clear remembered failures
plugins             Print registered plugin summaries
web                 Manage web server settings
irc                 View and manage irc connections
trakt               View and manage trakt authentication.
movie-list          View and manage movie lists
t411                view and manipulate the Torrent411 plugin database
database            Utilities to manage the FlexGet database
series              View and manipulate the series plugin database
archive             Search and manipulate the archive database
check               validate configuration file and print errors
history             View the history of entries that FlexGet has accepted
rejected            list or clear remembered rejections
inject              inject an entry from command line into tasks
```