= Interval =

Allows specifying minimum interval for task execution. If cron execution happens before interval is met the task is skipped.

Format: [n] [minutes|hours|days|months]

Example:

{{{
interval: 7 days
}}}