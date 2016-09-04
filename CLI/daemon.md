## [`daemon`](/Daemon)<a name="daemon"></a>
run continuously, executing tasks according to schedules defined in config

### actions
| Action | Option | Description |
| --- | --- | --- |
| `start` || Starts the daemon  |
| |`-d, -daemonize`| Causes process to daemonize after starting
| `stop`<ul><li>`--wait`</li></ul> | shutdown the running daemon <ul><li>wait for all queued tasks to finish before stopping daemon</li></ul> |
| `status` | check if a daemon is running |
| `reload` | causes a running daemon to reload the config from disk |

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