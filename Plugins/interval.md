= Interval =

Allows specifying minimum interval for task execution. If cron execution happens before interval is met the task is skipped.

Format: [n] [minutes|hours|days|months]

Example:

{{{
interval: 7 days
}}}

'''{{{NOTE:}}}''' This is probably not useful in daemon mode. If you would like to set up the frequency of task execution in daemon mode, see [wiki:Daemon#scheduling scheduling].