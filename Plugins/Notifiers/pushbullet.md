# *Pushbullet*
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; Pushbullet is a part of the [notifier](/Plugins/Notifiers) plugin system.
</div>

This plugin provides the ability to send flexget notifications via the cross-platform notification system called [Pushbullet](https://www.pushbullet.com/).

## Configuration

| Option |Type|  Description | Default |
| --- | ---| --- |---|
| **api_key**| text| User's API key. **Required**|
|device|text|Target a specific device. Can also be a list. 
|email|email|Target user's emails. Can also be a list. 
|channel|text|Target channel. Can also be a list. 
|url|URL|Notification URL | 

<div class="alert alert-info" role="info">
  
  <span class="glyphicon glyphicon-info-sign"></span>
  &nbsp; Only one of `email`, `device` or `channel` can be used per config
</div>

### Examples


### Send notification for each accepted entry
```yaml
notify:
  entries:
    via:
      - pushbullet:
          api_key: API_key
```


