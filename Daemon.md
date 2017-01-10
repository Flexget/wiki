# Daemon
FlexGet can be run in daemon mode, which means it will always run in the background, periodically running tasks on a schedule, or running the tasks initiated by another instance of FlexGet. Also see the [daemon CLI documentation](/CLI/daemon).

## Usage
To launch the FlexGet daemon, use the `start` command:
  
^*Note: Using the optional `-d` switch will send the FlexGet daemon to the background. Using `--autoreload-config` will force config reloads before task execution.*^
```YAML
flexget daemon start [-d, --autoreload-config]
```


To stop a currently running daemon you can use `stop`:
```
flexget daemon stop
```
To check the status of the flexget daemon you can use `status`:
```
flexget daemon status
```
To have the daemon reload the config file from disk you can use the `reload-config` command:
```
flexget daemon reload-config
```

#### Mac OS X note regarding `-d`
Due to an apparent bug in current versions, the `-d` command may [ticket:2427 cause Flexget to start but quit immediately on Mac OS X]. There are two work-arounds while the issue is looked into:
1. You can run the command, replacing `-d` with `&`. See [comment:7:ticket:2427 this comment] in the bug thread for details.
2. Use the app bundle [found here](https://github.com/tubedogg/FlexgetDaemon) to launch the daemon. Instructions can be found at that link as well. **This app bundle was not created, and is not maintained, by Flexget** and questions or issues regarding the app bundle should be directed to [the issues page](https://github.com/tubedogg/FlexgetDaemon/issues) there.
3. Launch the daemon at login using a Launch Agent (see [here](/Daemon/Startup#AsanOSXLaunchAgent)). This enables the daemon to be run in the background without the `-d` option and without an open Terminal window.

## Remote Execution
If you run `flexget execute` while a daemon is running, the execution will be sent to the running daemon, and either run immediately, or queued for execution after the current running task has finished. The log results of this execution will be sent back to the calling terminal for viewing as well. This means that if you are running a daemon, you need not worry about concurrent calls of `flexget execute` having problems due to the lock file.

## Starting the Daemon
In order to get the daemon to start automatically on system boot, see [here](/Daemon/Startup).

## Scheduling
The [scheduler plugin](/Plugins/Daemon/scheduler) is responsible for executing your tasks periodically. By default it will run all tasks once an hour when FlexGet is running in daemon mode. Please see the [scheduler documentation](/Plugins/Daemon/scheduler) for more information on setting up schedules.