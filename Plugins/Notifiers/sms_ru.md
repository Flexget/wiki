# [Notifiers](/Plugins/Notifiers) > SMS RU

<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; SMS RU can be is a part of the [notifier](/Plugins/Notifiers) plugin system.
</div>

This plugin provides the ability to send flexget notifications via the cross-platform notification system called [SMS RU](http://sms.ru/).

## Configuration

| Option |Type|  Description | Default |
| --- | ---| --- |---|
|phone_number|text|Phone number to SMS. **Required**
|password|text|Service password. **Required**

#### Example:
<div class="alert alert-warning" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; Examples show a specifc scenario usage of the [notify](/Plugins/notify) plugin. See its wiki for a more detailed usage exaplantion.
</div>

```yaml
notify:
  entries:
    via:
      - sms_ru:
          phone_number: 6534563456345
          password: PASSWORD
```

