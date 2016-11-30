# *SMS RU*

<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; SMS RU can be used as a part of [notifier](/Plugins/Notifiers) plugin system.
</div>

This plugin provides the ability to send flexget notifications via the cross-platform notification system called [SMS RU](http://sms.ru/).

## Configuration

| Option |Type|  Description | Default |
| --- | ---| --- |---|
|*phone_number*|text|Phone number to SMS. **Required**
|*password*|text|Service password. **Required**
|message|text| Notification message| Gets default from [notify](/Plugins/Notifiers/notify) plugin
| file_template | text|Name of the template file to use. See [notify](/Plugins/Notifiers/notify) plugin for more details|

#### Example:
```yaml
sms_ru:
  phone_number: 6534563456345
  password: PASSWORD
```

