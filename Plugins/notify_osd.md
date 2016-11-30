# *Notify-OSD*
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; Notify-OSD can be used as a part of [notifier](/Plugins/Notifiers) plugin system.
</div>

**`Requirement:`**
Must have a notification system like dbus for linux operating systems. Has been tested on Ubuntu 12.04 only!

## Configuration

| Option |Type|  Description | Default |
| --- | ---| --- |---|
|title|text|Notification title|Gets default from [notify](/Plugins/Notifiers/notify) plugin|
|message|text| Notification message| Gets default from [notify](/Plugins/Notifiers/notify) plugin
|timeout|numeric|Number of seconds to display notification|`4`
| file_template | text|Name of the template file to use. See [notify](/Plugins/Notifiers/notify) plugin for more details| 


**Syntax:**

```yaml
notify_osd:
  title: {{task_name}}
  message: {{title}}
```
<div class="alert alert-warning">
  
  <!--<span class="glyphicon glyphicon glyphicon-cog"></span>-->
  &nbsp; <strong>Warning!</strong> Please ensure you have a notification system on your distribution before enabling this option.
</div>


