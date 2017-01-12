# *Join*
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; Join can be used as a part of [notifier](/Plugins/Notifiers) plugin system.
</div>



This plugin provides the ability to send flexget notifications via the cross-platform notification system called [Join](https://joaoapps.com/join/).

## Configuration

| Option |Type|  Description | Default |
| --- | ---| --- |---|
| **api_key**| text| User's API key. Either this or `device` are **required.**| 
| **device**| text| Device ID. Can also be a list. Either this or `api_key` are **required.**|
|group|text|Sepcifed device group to send notification to. One of `all`, `android`, `chrome`, `windows10`, `phone`, `tablet` or `pc`. Requires using `api_key`|`all`
|url|URL|Notification URL | Gets default from [notify](/Plugins/Notifiers/notify) plugin
|icon|URL|Notification icon
|sms_number|text|Send an SMS to this nubmer using device (in addition to regular notification). Will use `message` as SMS body
|priority|numeric|Sets notification priority. Can be between -2 and 2.


#### Example
```yaml
join:
  api_key: API_LEY
```
Or:
```yaml
join:
  device: DEVICE
```

#### Advanced Example
```yaml
join:
  device: 
    - DEVICE1
    - DEVICE2
  group: windows10
  priority: 2
  url: http://server.example.com/path/to/downloader/ui
  icon: http://bla.com/image.jpg
  sms_number: '1800555555'
```
