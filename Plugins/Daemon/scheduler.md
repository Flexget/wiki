# [Daemon](/Daemon]) > Scheduler
The scheduler is a plugin for use in daemon mode which can execute tasks periodically.

## Configuration
To tell FlexGet how often it should execute your tasks, you can set up the `schedules` block in the config file. Note that unlike most plugins, `schedules` is one of the [top-level keys](/Configuration#top-level-keys) and is not indented under anything else.

Each schedule consists of a list of tasks to run, and an interval which they should be run at. If you run the daemon without specifying a schedules block, a default schedule of Every task, every hour is assumed.

**`Please Note:`** You may see a warning like the following when using schedules. You can safely ignore it.
```
2014-01-07 10:28 WARNING  manager                       Config line XX is likely missing ':' at the end
```

### Disabling
If you would like to run the daemon without any builtin schedules -- perhaps you are sending executions from cron or some other source -- you can turn off the scheduler like so:
```
schedules: no
```


### Tasks
Tasks can be specified as either a single task, or a list of tasks to execute. When specifying tasks, wildcards such as `*` (any characters), or `?` (any single character) can be used to match multiple tasks.

Note that if you specify multiple schedules containing the same task, including when matched by a wildcard, that task will be launched once for each schedule containing it.

### Period
You can define how often a schedule should run in one of two ways.

**Interval**

The easiest way is to specify an `interval`. Choose a unit of time and tell it how often the task should be run. The configuration format is as follows:
```
schedules:
  - tasks: [list, of, tasks]
    interval:
      <weeks|days|hours|minutes>: <#>
```
Examples:
```
schedules:
  # Run every task once an hour
  - tasks: '*'
    interval:
      hours: 1
  # Run task_a and task_b every 30 minutes
  - tasks: [task_a, task_b]
    interval:
      minutes: 30
```

**Schedule**

If you need a bit more control of when tasks should run, you can use the more advanced `schedule` key. This allows schedules to be defined very similarly to how you would in cron. The config format is:
```
schedules:
  - tasks: [list, of, tasks]
    schedule:
      minute: X
      hour: X
      day: X
      day_of_week: X
      week: X
      month: X
      year: X
```

All of the different units are optional, and support values like cron. For more details on the types of values that can be used for each of these fields, you can reference the [apscheduler](http://apscheduler.readthedocs.org/en/latest/modules/triggers/cron.html#expression-types) documentation. Here are some examples of different ways to set up a schedule:
```
schedules:
  # Run every 30 minutes on monday
  - tasks: [taskone, tasktwo]
    schedule:
      minute: "*/30"
      day_of_week: mon
  # Run at 22:05, 22:45, 23:05, 23:45
  - tasks: task3
    schedule:
      minute: 5,45
      hour: 22,23
  # Run every 15 minutes on tuesdays and thursdays between noon and 5 pm
  - tasks: task4
    schedule:
      day_of_week: tue,thu
      hour: 12-17
      minute: "*/15"
  # Run every 2 hours between 8am and 8pm
  - tasks: task5
    schedule:
      hour: 8-20/2
```
