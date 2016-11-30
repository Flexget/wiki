# *Pushbullet*
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; Pushbullet can be used as a part of [notifier](/Plugins/Notifiers) plugin system.
</div>



This plugin provides the ability to send flexget notifications via the cross-platform notification system called [Pushbullet](https://www.pushbullet.com/).

## Configuration

| Option |Type|  Description | Default |
| --- | ---| --- |---|
| **api_key**| text| User's API key. **Required**|
|device|text|Target a specific device. Can also be a list. 
|email|email|Target user's emails. Can also be a list. 
|channel|text|Target channel. Can also be a list. 
|title|text|Notification title|Gets default from [notify](/Plugins/Notifiers/notify) plugin|
|message|text| Notification message| Gets default from [notify](/Plugins/Notifiers/notify) plugin
|url|URL|Notification URL | Gets default from [notify](/Plugins/Notifiers/notify) plugin
| file_template | text|Name of the template file to use. See [notify](/Plugins/Notifiers/notify) plugin for more details| 

<div class="alert alert-info" role="info">
  
  <span class="glyphicon glyphicon-info-sign"></span>
  &nbsp; Only one of `email`, `device` or `channel` can be used per config
</div>

#### Example
```yaml
pushbullet:
  api_key: API_key
```

#### Advanced Example
```yaml
pushbullet:
  api_key: API_key
  device: 345623456
  device: mobile
  title: Downloading {{series_name}}
  message: Episode {{series_id}}
```


