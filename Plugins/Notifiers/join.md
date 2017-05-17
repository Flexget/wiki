# [Notifiers](/Plugins/Notifiers) > Join
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; Join is a part of the [notifier](/Plugins/Notifiers) plugin system.
</div>



This plugin provides the ability to send flexget notifications via the cross-platform notification system called [Join](https://joaoapps.com/join/).

## Configuration

| Option |Type|  Description | Default |
| --- | ---| --- |---|
| **api_key**| text| User's API key. **Required.**| 
| device| text| Device ID. Can also be a list. Can not select together with `group`|
| device_name| text| Device name. Can also be a list. |
|group|text|Sepcifed device group to send notification to. One of `all`, `android`, `chrome`, `windows10`, `phone`, `tablet` or `pc`. can not select together with `device`|`all`
|url|URL|Notification URL | Gets default from [notify](/Plugins/Notifiers/notify) plugin
|icon|URL|Notification icon
|sms_number|text|Send an SMS to this nubmer using device (in addition to regular notification). Will use `message` as SMS body
|priority|numeric|Sets notification priority. Can be between -2 and 2.


#### Examples
<div class="alert alert-warning" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; Examples show a specifc scenario usage of the [notify](/Plugins/notify) plugin. See its wiki for a more detailed usage exaplantion.
</div>

```yaml
notify:
  entries:
    via:
      - join:
          api_key: API_LEY
```


#### Advanced Example
```yaml
notify:
  entries:
    via:
      - join:
          api_key: KEY
          device: 
            - DEVICE1
            - DEVICE2
          group: windows10
          priority: 2
          url: http://server.example.com/path/to/downloader/ui
          icon: http://bla.com/image.jpg
          sms_number: '1800555555'
```
