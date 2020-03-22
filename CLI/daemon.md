## [CLI](/CLI) > [`daemon`](/Daemon)<a name="daemon"></a>
Run FlexGet continuously, executing tasks according to [schedules](/Plugins/Daemon/scheduler) defined in the [config file](/Configuration).

### Notes
Further information is available about [daemon operation](/Daemon).

### Sub-commands
| Sub-command | Option | Description |
| --- | --- | --- |
| `start` || Starts the daemon  |
| |`-d`, `--daemonize`| Causes process to daemonize after starting
| |`--autoreload-config` | Automatically reload the config from disk if the daemon detects any changes |
| | `--disable-tray-icon` | Disable the tray icon from loading |
| `stop` || Shutdown the running daemon |
|| `--wait`| Wait for all queued tasks to finish before stopping daemon |
| `status` || Check if a daemon is running |
| `reload-config` || Causes a running daemon to reload the config from disk |

### examples
```bash
#starts the FlexGet daemon
$ flexget daemon start

#starts the FlexGet daemon and daemonizes the process
$ flexget daemon start -d

#stops the FlexGet daemon
$ flexget daemon stop

#stops the FlexGet daemon but waits for all tasks to finish
$ flexget daemon stop --wait
```