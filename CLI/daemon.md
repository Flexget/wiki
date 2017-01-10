## [`daemon`](/Daemon)<a name="daemon"></a>
run continuously, executing tasks according to schedules defined in config

### actions
| Action | Option | Description |
| --- | --- | --- |
| `start` || Starts the daemon  |
| |`-d, --daemonize`| Causes process to daemonize after starting
| |`--autoreload-config` | automatically reload the config from disk if the daemon detects any changes |
| `stop` || shutdown the running daemon |
|| `--wait`| wait for all queued tasks to finish before stopping daemon |
| `status` || check if a daemon is running |
| `reload` || causes a running daemon to reload the config from disk |
| `enable-autoreload` || enables automatic config reload from disk |
| `disable-autoreload` || disables automatic config reload from disk |

### examples
```bash
#starts the FlexGet daemon
flexget daemon start
#starts the FlexGet daemon and daemonizes the process
flexget daemon start -d
#stops the FlexGet daemon
flexget daemon stop
#stops the FlexGet daemon but waits for all tasks to finish
flexget daemon stop --wait
```

### Related articles
* [CUI / Command line interface overview](/CLI)
* [`daemon` Wiki article](/Daemon)