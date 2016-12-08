# Notify crash
Sends notification to [notifer](/Plugins/Notifiers) plugins on task crash.

## Schema
```text
notify_crash:
  to: <NOTIFIER_PLUGINS> [List of at least one notifer plugins, the same plugin can be used more than once, Required.]
```
Unlike [notify](/Plugins/Notifiers/notify) plugin, you can not set global attributes, only per plugin ones.
### Usage:
```yaml
tasks:
  download_task:
    rss: http://stuff.com
    accept_all: yes
    download: /downloads/
    notify_crash:
      to:
        - pushover:
            user_key: user_key
```
This will send a notification using the following defaults:  
`title` -  `Task {{ task_name }} has crashed!`  
`message` - `Reason: {{ task.abort_reason }}`

You could also use `notify_crash` in a global template as such:
```yaml
templates:
  global:
    notify_crash:
      to:
        - pushover:
            user_key: user_key
```
Doing this will let you be notified of a crash in any task.