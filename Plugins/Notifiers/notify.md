# Notify

Use this plugin to send notification to one or more [notifer](/Plugins/Notifers) plugins.
This plugin runs on task exit and can be configured extensively

### Schema:

```text
notify:
  to: <NOTIFIER_PLUGINS> [List of at least one notifer plugins, the same plugin can be used more than once, Required.]
  scope: <`task` or `entries`> [Defines the scope of the data to be used in the notification. Default is `entries`.]
  what: <'entries', 'accepted', 'rejected', 'failed', 'undecided'> [The data to iterate on, relevant to `entries` scope only. One or more can be used. Default is `accepted`]
  title: <STRING> Global title to be used by all notifiers. 
  message: <STRING> Global message to be used by all notifiers. 
  url: <STRING> Global URL to be used by all notifiers. 
  file_template: File template to be used, will replace `message` value if present.
```
### Basic usage:
Looking at the schema, we can see that by default, using the minimal `notify` setting, a notifier will be defined as such:
```yaml
tasks:
  download_task:
    rss: http://stuff.com
    accept_all: yes
    download: /downloads/
    notify:
      to
        - pushover:
            user_key: user_key
```
This will use `entries` scope and send a notification for each `accepted` one. It is functionally similar to direcly calling the notifier as such:
