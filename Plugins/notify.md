# Notify
This plugin can be used to send messages about different events during task execution. These messages can be delivered by one (or more) of the [notification delivery plugins](/Plugins/Notifiers). There are 3 main categories of message this plugin can send:

## Entries
Sends a notification for each accepted entry in a task. (It can alternatively be configred to send messages about rejected or failed entries if desired.)

## Task
Sends a notification when the task completes with either accepted or failed entries.

## Abort
Sends a notification when the task aborts.