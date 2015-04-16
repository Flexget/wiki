= Daemon =

!FlexGet can be run in daemon mode, which means it will always run in the background, periodically running tasks on a schedule, or running the tasks initiated by another instance of !FlexGet.

== Usage ==
To launch the !FlexGet daemon, use the `start` command:
[[BR]]
^''Note: Using the optional `-d` switch will send the !FlexGet daemon to the background.''^
{{{
flexget daemon start [-d]
}}}


To stop a currently running daemon you can use `stop`:
{{{
flexget daemon stop
}}}
To check the status of the flexget daemon you can use `status`:
{{{
flexget daemon status
}}}
To have the daemon reload the config file from disk you can use the `reload` command:
{{{
flexget daemon reload
}}}

==== Mac OS X note regarding `-d` ====
Due to an apparent bug in current versions, the `-d` command may [ticket:2427 cause Flexget to start but quit immediately on Mac OS X]. There are two work-arounds while the issue is looked into:
1. You can run the command, replacing `-d` with `&`. See [comment:7:ticket:2427 this comment] in the bug thread for details.
2. Use the app bundle [https://github.com/tubedogg/FlexgetDaemon found here] to launch the daemon. Instructions can be found at that link as well. '''This app bundle was not created, and is not maintained, by Flexget''' and questions or issues regarding the app bundle should be directed to [https://github.com/tubedogg/FlexgetDaemon/issues the issues page] there.
3. Launch the daemon at login using a Launch Agent (see [wiki:Daemon/Startup#AsanOSXLaunchAgent here]). This enables the daemon to be run in the background without the `-d` option and without an open Terminal window.

== Remote Execution ==
If you run `flexget execute` while a daemon is running, the execution will be sent to the running daemon, and either run immediately, or queued for execution after the current running task has finished. The log results of this execution will be sent back to the calling terminal for viewing as well. This means that if you are running a daemon, you need not worry about concurrent calls of `flexget execute` having problems due to the lock file.

== Starting the Daemon ==

In order to get the daemon to start automatically on system boot, see [wiki:Daemon/Startup here].

== Scheduling ==

The [wiki:Plugins/Daemon/scheduler scheduler plugin] is responsible for executing your tasks periodically. By default it will run all tasks once an hour when !FlexGet is running in daemon mode. Please see the [wiki:Plugins/Daemon/scheduler scheduler documentation] for more information on setting up schedules.