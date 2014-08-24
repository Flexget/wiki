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

==== Mac OS X note regarding -d ====
Due to an apparent bug in current versions, the ```-d``` command may [ticket:2427 cause Flexget to start but quit immediately on Mac OS X]. There are two work-arounds while the issue is looked into:
1. You can run the command, replacing ```-d``` with ```&```. See [comment:7:ticket:2427 this comment] in the bug thread for details.
2. Use the app bundle [https://github.com/tubedogg/FlexgetDaemon found here] to launch the daemon. Instructions can be found at that link as well. '''This app bundle was not created, and is not maintained, by Flexget''' and questions or issues regarding the app bundle should be directed to [https://github.com/tubedogg/FlexgetDaemon/issues the issues page] there.


== Scheduling ==

To tell !FlexGet how often it should execute your tasks, you can set up the `schedules` block in the config file. Each schedule consists of a list of tasks to run, and an interval which they should be run at. When specifying tasks, wildcards such as `*` (any characters), or `?` (any single character) can be used. If you run the daemon without specifying a schedules block, a default schedule of Every task, every hour is assumed. The configuration format is as follows:
{{{
schedules:
  - tasks: [list, of, tasks]
    interval:
      <weeks|days|hours|minutes>: <#>
      on_day: <monday|tuesday...>
      at_time: HH:MM [am|pm]  # 24h time can also be used
}}}
The `at_time` option can only be used when the interval is `days` or larger, and the `on_day` option can only be used when the interval is `weeks`. When only running a single task, the list notation need not be used. Here are some examples:
{{{
schedules:
  # Run every task once an hour
  - tasks: '*'
    interval:
      hours: 1
  # Run task_a and task_b every 30 minutes
  - tasks: [task_a, task_b]
    interval:
      minutes: 30
  # Run any task starting with 'weekly_' on tuesdays at 1 pm
  - tasks: 'weekly_*'
    interval:
      weeks: 1
      on_day: tuesday
      at_time: 1:00 pm
}}}

If you would like to run the daemon without any builtin schedules, (perhaps you are still sending executions from cron, or some other source,) you can turn off the scheduler like so:
{{{
schedules: no
}}}

'''Please Note:''' You may see a warning like the following when using schedules, for now you can safely ignore it.
{{{
2014-01-07 10:28 WARNING  manager                       Config line 11 is likely missing ':' at the end
}}}

== Remote Execution ==
If you run `flexget execute` while a daemon is running, the execution will be sent to the running daemon, and either run immediately, or queued for execution after the current running task has finished. The log results of this execution will be sent back to the calling terminal for viewing as well. This means that if you are running a daemon, you need not worry about concurrent calls of `flexget execute` having problems due to the lock file.

== Starting the Daemon ==

In order to get the daemon to start automatically on system boot, see [wiki:Daemon/Startup here].