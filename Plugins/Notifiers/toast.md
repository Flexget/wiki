# Toast
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; Toast is a part of [notifier](/Plugins/Notifiers) plugin system.
</div>

**`Requirement:`**
Either:
- Must have a notification system like dbus for linux operating systems. Has been tested on Ubuntu 12.04 only!
- Preliminary support for Windows notifications. Not heavily tested yet.


## Configuration

| Option |Type|  Description | Default |
| --- | ---| --- |---|
|timeout|numeric|Number of seconds to display notification|`4`


**Syntax:**

```yaml
toast: yes
# or
toast:
  timeout: 5
```
<div class="alert alert-warning">
  
  <!--<span class="glyphicon glyphicon glyphicon-cog"></span>-->
  &nbsp; <strong>Warning!</strong> Please ensure you have a notification system on your distribution before enabling this option.
</div>


