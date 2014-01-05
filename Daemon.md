= Daemon =

!FlexGet can be run in daemon mode, which means it will always run in the background, periodically running tasks on a schedule, or running the tasks initiated by another instance of !FlexGet.

To launch the !FlexGet daemon, use the command:
{{{
flexget daemon start
}}}

== Scheduling ==

To tell !FlexGet how often it should execute your tasks, you can set up the `schedules` block in the config file. Each schedule consists of a list of tasks to run, and an interval which they should be run at. When specifying tasks, wildcards such as `*` (any characters), or `?` (any single character) can be used. If you run the daemon without specifying a schedules block, a default schedule The configuration format is as follows:
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
  - tasks: *
    interval:
      hours: 1
  # Run task_a and task_b every 30 minutes
  - tasks: [task_a, task_b]
    interval:
      minutes: 30
  # Run any task starting with 'weekly_' on tuesdays at 1 pm
  - tasks: weekly_*
    interval:
      weeks: 1
      on_day: tuesday
      at_time: 1:00 pm
}}}
If you would like to run the daemon without any builtin schedules, (perhaps you are still sending executions from cron, or some other source,) you can configure it with an empty list, like so:
{{{
schedules: []
}}}

== Remote Execution ==
If you run `flexget execute` while a daemon is running, the execution will be sent to the running daemon, and either run immediately, or queued for execution after the current running task has finished. The log results of this execution will be sent back to the calling terminal for viewing as well. This means that if you are running a daemon, you need not worry about concurrent calls of `flexget execute` having problems due to the lock file.